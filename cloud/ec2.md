---
title: EC2
parent: Cloud Computing
nav_order: 91
layout: default
---

## EC2 (Elastic Compute Cloud)

Amazon EC2 (Elastic Compute Cloud) is a web service that provides resizable compute capacity in the cloud. It's essentially virtual servers that you can rent from AWS. You can use EC2 instances to run applications, host websites, process data, and perform any other tasks you would do on a traditional server.

---

### Key Concepts

- **Instance:** A virtual server in the AWS cloud. You choose the operating system, instance type (CPU, memory, storage, networking), and other settings.
- **Instance Type:** Defines the hardware configuration of your instance (e.g., `t2.micro`, `m5.large`, `c5.xlarge`). Different instance types are optimized for different workloads (general purpose, compute-intensive, memory-intensive, etc.). AWS offers a _huge_ variety of instance types.
- **AMI (Amazon Machine Image):** A template that contains the software configuration (operating system, application server, applications) required to launch an instance. You can use pre-built AMIs from AWS, the AWS Marketplace, or create your own.
- **Security Group:** A virtual firewall that controls inbound and outbound traffic to your instance. You define rules to allow or deny traffic based on protocol, port, and source/destination IP address.
- **Key Pair:** A set of security credentials used to connect to your instance securely via SSH. You create a key pair in AWS, download the private key file (e.g., `.pem` file), and use it to authenticate when connecting. _Keep your private key file secure!_
- **Elastic IP Address:** A static public IP address that you can associate with an instance. Unlike the default public IP address assigned to an instance, an Elastic IP address remains associated with your account even if you stop and restart the instance.
- **EBS (Elastic Block Storage):** Persistent block storage volumes that you can attach to your EC2 instances. Think of them as virtual hard drives. EBS volumes persist independently of the instance's lifecycle.
- **Region:** A geographical location where AWS data centers are located (e.g., `us-east-1` (N. Virginia), `eu-west-2` (London)). You choose a region when launching an instance.
- **Availability Zone (AZ):** A distinct location within a region that is engineered to be isolated from failures in other Availability Zones. You can launch instances in multiple AZs for high availability.
- **IAM Roles**: Secure way to grant permissions to applications running on your EC2 instances.
- **User Data:** You can pass user data to an instance which can be used to perform automated configurations.

---

### Launching an EC2 Instance (Simplified Example - using the AWS CLI)

This example demonstrates launching a basic Ubuntu instance using the AWS CLI (Command Line Interface). You'll need to have the AWS CLI installed and configured with your AWS credentials. This is a _simplified_ example for illustration; in a real-world scenario, you'd likely use infrastructure-as-code tools like Terraform or CloudFormation.

1.  **Create a Key Pair (if you don't already have one):**

    ```bash
    aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem
    chmod 400 MyKeyPair.pem  # Set permissions on the private key file (very important!)
    ```

2.  **Find an AMI ID:** You'll need an AMI ID for the operating system you want to use. You can find AMI IDs in the AWS Management Console (EC2 service) or using the CLI. This example uses an Ubuntu 22.04 AMI ID for the `us-east-1` region (you'll need to find the appropriate AMI for your region and desired OS):

    ```bash
    # (Example - find the latest Ubuntu 22.04 AMI - this command is complex, but demonstrates the power of the CLI)
    ami_id=$(aws ec2 describe-images \
        --owners amazon \
        --filters "Name=name,Values=ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*" \
        --query 'Images[*].[ImageId,Name,CreationDate]' \
        --output text | sort -k 3 -r | head -n 1 | awk '{print $1}')
    echo "Using AMI ID: $ami_id"

    ```

3.  **Create a Security Group (allows SSH access):**

    ```bash
    sg_id=$(aws ec2 create-security-group --group-name MySecurityGroup --description "Allow SSH access" --query 'GroupId' --output text)
    aws ec2 authorize-security-group-ingress --group-id $sg_id --protocol tcp --port 22 --cidr 0.0.0.0/0
    ```

    _Note:_ `0.0.0.0/0` allows access from any IP address. In production, you should restrict this to specific IP addresses or ranges for security.

4.  **Launch the Instance:**

    ```bash
    instance_id=$(aws ec2 run-instances \
        --image-id $ami_id \
        --count 1 \
        --instance-type t2.micro \
        --key-name MyKeyPair \
        --security-group-ids $sg_id \
        --query 'Instances[0].InstanceId' \
        --output text)
    echo "Launched instance with ID: $instance_id"

    ```

    _Explanation:_

    - `--image-id`: The AMI ID.
    - `--count 1`: Launch one instance.
    - `--instance-type t2.micro`: Use the `t2.micro` instance type (free tier eligible).
    - `--key-name MyKeyPair`: Use the key pair you created.
    - `--security-group-ids`: Use the security group you created.

5.  **Get the Public IP Address:**

    ```bash
    public_ip=$(aws ec2 describe-instances --instance-ids $instance_id --query 'Reservations[*].Instances[*].PublicIpAddress' --output text)
    echo "Public IP Address: $public_ip"
    ```

6.  **Connect to the Instance (via SSH):**

    ```bash
    ssh -i MyKeyPair.pem ubuntu@$public_ip
    ```

    _Note:_ The username (`ubuntu` in this case) depends on the AMI you used.

7.  **Terminate instance:**

    ```bash
    aws ec2 terminate-instances --instance-ids $instance_id
    ```
