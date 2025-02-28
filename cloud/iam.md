---
title: IAM
parent: Cloud Computing
nav_order: 93
layout: default
---

## IAM (Identity and Access Management)

AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources. It's a fundamental part of AWS security and is _essential_ for managing access in a multi-user environment.

---

### Key Concepts

- **Users:** Represent individual people or applications that need to access AWS resources. Users have long-term credentials (username/password, access keys).
- **Groups:** Collections of IAM users. You can assign permissions to groups, and all users in the group inherit those permissions. This simplifies managing permissions for multiple users.
- **Roles:** Similar to users, but _not_ associated with a specific person. Roles are intended to be assumed by anyone who needs them (e.g., an EC2 instance, a Lambda function, a user from another AWS account). Roles provide _temporary_ security credentials. This is a best practice for granting access to AWS services.
- **Policies:** JSON documents that define permissions. Policies specify what actions are allowed or denied on which resources. You attach policies to users, groups, or roles.
- **Permissions:** Specific actions that a user, group, or role is allowed to perform (e.g., `s3:GetObject`, `ec2:RunInstances`, `iam:CreateUser`).
- **Resources:** The AWS objects that users interact with (e.g., EC2 instances, S3 buckets, DynamoDB tables).
- **Principal:** The entity (user, group, role, or service) that is requesting access to a resource.
- **MFA (Multi-Factor Authentication):** An extra layer of security that requires users to provide more than just a password to authenticate (e.g., a code from a mobile app, a security key). MFA is _highly recommended_ for all IAM users.
- **Root User**: When you first create an AWS account, you start with root user. The root user can do everything and it is not a good practice to work with root user.

---

### Key Principles

- **Least Privilege:** Grant only the minimum permissions required to perform a task. Avoid granting overly broad permissions (like `*:*`, which allows all actions on all resources). Start with minimal permissions and add more as needed.
- **Use Groups and Roles:** Manage permissions through groups and roles whenever possible. Avoid attaching policies directly to individual users.
- **Use IAM Roles for AWS Services:** Don't store AWS credentials in your application code or on your EC2 instances. Use IAM roles to grant temporary credentials to applications running on AWS services.
- **Enable MFA:** Enable multi-factor authentication for all IAM users, especially those with administrative privileges.

---

### Example: Creating an IAM User with Limited S3 Access (using the AWS CLI)

This example shows how to create an IAM user, create a policy that grants read-only access to a specific S3 bucket, and attach the policy to the user.

1.  **Create the IAM User:**

    ```bash
    aws iam create-user --user-name S3ReadOnlyUser
    ```

2.  **Create a Policy (save this as `s3-read-only-policy.json`):**

    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": ["s3:GetObject", "s3:ListBucket"],
          "Resource": [
            "arn:aws:s3:::your-bucket-name" /* Replace with your bucket's ARN */,
            "arn:aws:s3:::your-bucket-name/*" /* Replace with your bucket's ARN */
          ]
        }
      ]
    }
    ```

    _Explanation:_
    _ `"Version": "2012-10-17"`: The version of the policy language.
    _ `"Statement": [...]`: An array of statement objects.

    - `"Effect": "Allow"`: Specifies that the statement _allows_ access.
    - `"Action": [...]`: An array of actions that are allowed. `s3:GetObject` allows downloading objects, and `s3:ListBucket` allows listing the objects in the bucket.
    - `"Resource": [...]`: An array of ARNs (Amazon Resource Names) that specify the resources the policy applies to. This policy allows access to the specified bucket _and_ all objects within the bucket (`/*`).

3.  **Create the Policy in IAM:**

    ```bash
    aws iam create-policy --policy-name S3ReadOnlyPolicy --policy-document file://s3-read-only-policy.json
    ```

4.  **Attach the Policy to the User:**

    ```bash
    aws iam attach-user-policy --policy-arn arn:aws:iam::YOUR_ACCOUNT_ID:policy/S3ReadOnlyPolicy --user-name S3ReadOnlyUser
    # Replace YOUR_ACCOUNT_ID with your actual AWS account ID.  You can find your account ID in the AWS console.
    ```

5.  **Create Access Key:**

```bash
  aws iam create-access-key --user-name S3ReadOnlyUser
```
