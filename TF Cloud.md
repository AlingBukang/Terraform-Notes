# Terraform Cloud

Terraform Cloud is an application that helps teams use Terraform together. It extends the open-source Terraform CLI's capabilities to make it easier to collaborate, govern, and automate infrastructure workflows. Key features include:

- **Collaboration and Governance**: Enables teams to collaborate on shared Terraform state and modules, with governance controls to ensure changes are reviewed and approved.
- **Remote State Management**: Provides secure, versioned storage for Terraform state files, with locking to prevent conflicts.
- **Secure Variable Storage**: Stores sensitive information like cloud credentials, securely and access them as environment variables in Terraform runs.
- **Plan and Apply with Policy Controls**: Allows you to set policies that must be passed before changes can be applied, helping to enforce best practices and prevent mistakes.
- **Team Access Controls**: Manages access to resources based on individual roles and responsibilities.
- **Audit Logging**: Keeps a detailed log of all actions and changes for compliance and troubleshooting.
- **API-Driven Workflow**: Enables integration with your existing CI/CD pipeline and other tools via a robust API.
- **Cost Estimation**: Provides a cost estimate for proposed infrastructure changes before they are applied.
- **Sentinel Policy as Code Framework**: Allows you to define fine-grained, logic-based policy decisions, and apply them to any stage of the provisioning process.
- **Private Module Registry**: Allows you to share and reuse Terraform modules across your organization.
- **SSO/SAML**: Supports single sign-on (SSO) for managing user access.
- **Self-Hosted Agents**: Allows you to execute Terraform operations in a controlled, isolated environment within your own network infrastructure.

## Managing AWS IAM with Terraform

Terraform is a powerful tool for managing infrastructure in the cloud, and it can also be used to manage AWS Identity and Access Management (IAM) resources.
Here's an example of how to create an IAM user and attach a policy to it using Terraform:

```yml
# Configure the AWS Provider
provider "aws" {
    region = "us-west-2"
}

# Create an IAM user
resource "aws_iam_user" "name" {
    name = "username"
    tags = {
        Description = "Description"
    }
}

# Define an IAM policy
resource "aws_iam_policy" "admin" {
    name = "admin"
    policy = <<EOF
    {
        "Statement" : [
            {
                "Effect": "Allow",
                "Action": "",
                "Resource": ""
            }
        ]
    }
    EOF
}

# Attach the policy to the user
resource "aws_iam_user_policy_attachment" "admin" {
    user = aws_iam_user.admin.name
    policy_arn = aws_iam_policy.admin.arn
}
```

In this example, we first configure the AWS provider with the desired region. Then, we create an IAM user with the `aws_iam_user` resource. We also define an IAM policy with the `aws_iam_policy` resource, and finally, we attach the policy to the user with the `aws_iam_user_policy_attachment` resource.

Remember to replace the placeholders in the `Action` and `Resource` fields of the policy with the actual AWS service actions and resources you want to allow.
