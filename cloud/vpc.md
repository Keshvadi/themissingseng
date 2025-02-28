---
title: VPC
parent: Cloud Computing
nav_order: 95
layout: default
---

## VPC (Virtual Private Cloud)

Amazon Virtual Private Cloud (VPC) lets you provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways. Essentially, a VPC is your private network within AWS.

---

### Key Concepts

- **VPC:** A virtual network dedicated to your AWS account. It's logically isolated from other virtual networks in the AWS Cloud.
- **Subnet:** A range of IP addresses within your VPC. You launch resources (like EC2 instances) into specific subnets. Subnets can be _public_ (have a route to the internet) or _private_ (no direct route to the internet).
- **CIDR Block (Classless Inter-Domain Routing):** A way of representing a range of IP addresses. You define a CIDR block for your VPC and for each subnet. (e.g., `10.0.0.0/16` for the VPC, `10.0.1.0/24` for a subnet).
- **Route Table:** A set of rules, called routes, that determine where network traffic from your subnet or gateway is directed.
- **Internet Gateway (IGW):** A VPC component that allows communication between instances in your VPC and the internet. A subnet is considered "public" if it has a route table entry that directs traffic to an Internet Gateway.
- **NAT Gateway (Network Address Translation):** Allows instances in a _private_ subnet to connect to the internet (e.g., for software updates) or other AWS services, but prevents the internet from initiating connections with those instances. NAT Gateways are managed by AWS and provide better availability and bandwidth than NAT instances.
- **NAT Instance:** An EC2 instance that you configure to perform network address translation. Less common than NAT Gateways now, as NAT Gateways are easier to manage and more scalable.
- **Security Group:** Acts as a virtual firewall for your instances to control inbound and outbound traffic. Security groups act at the instance level.
- **Network ACL (NACL):** An optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of _one or more subnets_. NACLs act at the subnet level. They are _stateless_, meaning you need to explicitly allow both inbound and outbound traffic.
- **VPC Peering:** A connection between two VPCs that enables you to route traffic between them using private IP addresses. Useful for connecting VPCs within the same AWS account or across different accounts.
- **VPC Endpoints:** Enable you to privately connect your VPC to supported AWS services and VPC endpoint services powered by AWS PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.
- **Flow Logs:** Capture information about the IP traffic going to and from network interfaces in your VPC. Flow logs can help you with tasks like troubleshooting connectivity issues, monitoring network traffic, and identifying security threats.
- **Default VPC**: AWS creates a default VPC in each region.

---

### Example: Creating a Simple VPC with Public and Private Subnets (using the AWS CLI)

This example demonstrates creating a basic VPC with one public subnet and one private subnet. This is a common setup for web applications, where the web servers are in the public subnet and the database servers are in the private subnet.

1.  **Create the VPC:**

    ```bash
    vpc_id=$(aws ec2 create-vpc --cidr-block 10.0.0.0/16 --query 'Vpc.VpcId' --output text)
    echo "VPC ID: $vpc_id"
    ```

2.  **Create a Public Subnet:**

    ```bash
    public_subnet_id=$(aws ec2 create-subnet --vpc-id $vpc_id --cidr-block 10.0.1.0/24 --availability-zone us-east-1a --query 'Subnet.SubnetId' --output text)
    echo "Public Subnet ID: $public_subnet_id"
    ```

    (Choose an appropriate Availability Zone for your region).

3.  **Create a Private Subnet:**

    ```bash
    private_subnet_id=$(aws ec2 create-subnet --vpc-id $vpc_id --cidr-block 10.0.2.0/24 --availability-zone us-east-1a --query 'Subnet.SubnetId' --output text)
    echo "Private Subnet ID: $private_subnet_id"
    ```

4.  **Create an Internet Gateway:**

    ```bash
    igw_id=$(aws ec2 create-internet-gateway --query 'InternetGateway.InternetGatewayId' --output text)
    aws ec2 attach-internet-gateway --vpc-id $vpc_id --internet-gateway-id $igw_id
    echo "Internet Gateway ID: $igw_id"
    ```

5.  **Create a Route Table for the Public Subnet:**

    ```bash
    public_rt_id=$(aws ec2 create-route-table --vpc-id $vpc_id --query 'RouteTable.RouteTableId' --output text)
    aws ec2 create-route --route-table-id $public_rt_id --destination-cidr-block 0.0.0.0/0 --gateway-id $igw_id
    aws ec2 associate-route-table --route-table-id $public_rt_id --subnet-id $public_subnet_id
    echo "Public Route Table ID: $public_rt_id"
    ```

6.  **Create a NAT Gateway (for the Private Subnet to access the internet):**

    - First, allocate an Elastic IP address:

      ```bash
      eip_allocation_id=$(aws ec2 allocate-address --domain vpc --query 'AllocationId' --output text)
      echo "Elastic IP Allocation ID: $eip_allocation_id"
      ```

    - Then, create the NAT Gateway:

      ```bash
      nat_gw_id=$(aws ec2 create-nat-gateway --subnet-id $public_subnet_id --allocation-id $eip_allocation_id --query 'NatGateway.NatGatewayId' --output text)
      echo "NAT Gateway ID: $nat_gw_id"
      ```

      _Note:_ NAT Gateways incur charges. Remember to delete it when you're finished if you don't need it.

7.  **Create a Route Table for the Private Subnet:**

    ```bash
    private_rt_id=$(aws ec2 create-route-table --vpc-id $vpc_id --query 'RouteTable.RouteTableId' --output text)
    # Wait for NAT Gateway to become available (this can take a few minutes):
    aws ec2 wait nat-gateway-available --nat-gateway-ids $nat_gw_id
    aws ec2 create-route --route-table-id $private_rt_id --destination-cidr-block 0.0.0.0/0 --nat-gateway-id $nat_gw_id
    aws ec2 associate-route-table --route-table-id $private_rt_id --subnet-id $private_subnet_id
    echo "Private Route Table ID: $private_rt_id"
    ```

8.  **Delete the created resources:**

```bash
# Disassociate and delete routes and route tables
aws ec2 disassociate-route-table --association-id $(aws ec2 describe-route-tables --route-table-ids $private_rt_id --query 'RouteTables[0].Associations[0].RouteTableAssociationId' --output text)
aws ec2 delete-route-table --route-table-id $private_rt_id
aws ec2 disassociate-route-table --association-id $(aws ec2 describe-route-tables --route-table-ids $public_rt_id --query 'RouteTables[0].Associations[0].RouteTableAssociationId' --output text)
aws ec2 delete-route-table --route-table-id $public_rt_id

# Detach and delete internet gateway
aws ec2 detach-internet-gateway --internet-gateway-id $igw_id --vpc-id $vpc_id
aws ec2 delete-internet-gateway --internet-gateway-id $igw_id

# Delete NAT gateway and release Elastic IP
aws ec2 delete-nat-gateway --nat-gateway-id $nat_gw_id
aws ec2 wait nat-gateway-deleted --nat-gateway-ids $nat_gw_id # Wait for deletion
aws ec2 release-address --allocation-id $eip_allocation_id

# Delete subnets
aws ec2 delete-subnet --subnet-id $public_subnet_id
aws ec2 delete-subnet --subnet-id $private_subnet_id

# Delete VPC
aws ec2 delete-vpc --vpc-id $vpc_id
```
