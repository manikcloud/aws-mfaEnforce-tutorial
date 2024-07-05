# AWS MFA Enforcement Tutorial

In today's cloud-driven world, securing access to your AWS resources is more critical than ever. One effective way to enhance security is by enforcing Multi-Factor Authentication (MFA) for all IAM users. This additional layer of protection significantly reduces the risk of unauthorized access. In this guide, we will walk you through setting up MFA enforcement for IAM users using AWS CloudFormation and Terraform.

For a detailed step-by-step guide, visit the full article on [Medium](https://varunmanik1.medium.com/enforcing-mfa-for-aws-iam-users-with-cloudformation-terraform-2be6cb67a68c).

## Objectives

1. **Create an IAM group** that enforces MFA for all its members.
2. **Attach a policy** to this group that requires users to enable MFA before they can access AWS resources.
3. **Allow users to manage their own IAM settings** (passwords, access keys, signing certificates, SSH public keys, and MFA devices) while enforcing MFA for all other actions.
4. **Ensure seamless MFA setup** so that users can easily enable MFA upon their next login.

## Prerequisites

- Basic knowledge of AWS IAM and infrastructure as code (IaC) tools.
- AWS CLI installed and configured on your local machine.
- Terraform installed on your local machine (for the Terraform section).
- Necessary permissions to create IAM roles, policies, and groups in your AWS account.

## AWS CloudFormation Instructions

1. **Define the CloudFormation Template**
   - Save the YAML content to a file named `enforce-mfa.yaml`.

2. **Deploy the CloudFormation Stack**
   - Use the AWS CLI to deploy the CloudFormation stack:
     ```sh
     aws cloudformation create-stack --stack-name EnforceMFAStack --template-body file://enforce-mfa.yaml --capabilities CAPABILITY_NAMED_IAM
     ```

3. **Add Users to the MFAEnforcedGroup**
   - After deploying the stack, add users to the `MFAEnforcedGroup` using the AWS CLI:
     ```sh
     aws iam add-user-to-group --group-name MFAEnforcedGroup --user-name <user1>
     aws iam add-user-to-group --group-name MFAEnforcedGroup --user-name <user2>
     # Repeat for other users
     ```

4. **Verify MFA Enforcement**
   - Users in the `MFAEnforcedGroup` will need to enable MFA to access AWS resources. Here’s how users can set up MFA:
     1. Log in to the AWS Management Console.
     2. Navigate to the IAM section.
     3. Go to the "Users" section and select your username.
     4. Click on the "Security credentials" tab.
     5. Scroll down to the "Assigned MFA device" section and click "Manage".
     6. Follow the instructions to assign a virtual MFA device (e.g., using Google Authenticator).

5. **Test After Enabling MFA**
   - Once MFA is enabled, users can log out and log back in to verify they can access AWS resources as usual.

## Terraform Instructions

1. **Define the Terraform Configuration**
   - Create a file named `main.tf` with the necessary Terraform code.

2. **Initialize Terraform**
   - Run the following commands to initialize Terraform and apply the configuration:
     ```sh
     terraform init
     terraform apply
     ```

3. **Add Users to the MFAEnforcedGroup**
   - Use the AWS CLI to add users to the `MFAEnforcedGroup`:
     ```sh
     aws iam add-user-to-group --group-name MFAEnforcedGroup --user-name <user1>
     aws iam add-user-to-group --group-name MFAEnforcedGroup --user-name <user2>
     # Repeat for other users
     ```

4. **Verify MFA Enforcement**
   - Users in the `MFAEnforcedGroup` will need to enable MFA to access AWS resources. Here’s how users can set up MFA:
     1. Log in to the AWS Management Console.
     2. Navigate to the IAM section.
     3. Go to the "Users" section and select your username.
     4. Click on the "Security credentials" tab.
     5. Scroll down to the "Assigned MFA device" section and click "Manage".
     6. Follow the instructions to assign a virtual MFA device (e.g., using Google Authenticator).

5. **Test After Enabling MFA**
   - Once MFA is enabled, users can log out and log back in to verify they can access AWS resources as usual.

## Conclusion

By following this guide, you will enhance the security of your AWS environment by enforcing MFA for all IAM users. Using AWS CloudFormation and Terraform, you can automate this process, ensuring consistency and ease of management. This approach not only protects your AWS resources with an additional layer of security but also empowers users to manage their own IAM settings without compromising security. Implementing MFA is a best practice that helps safeguard your infrastructure against unauthorized access and potential security breaches.

For a detailed step-by-step guide, visit the full article on [Medium](https://varunmanik1.medium.com/enforcing-mfa-for-aws-iam-users-with-cloudformation-terraform-2be6cb67a68c).
