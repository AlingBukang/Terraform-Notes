# Terraform Workspaces

Terraform Workspaces provide an efficient way to manage multiple environments (like dev, staging, prod) with the same configuration. Each workspace has its own separate state file, allowing resources within each workspace to be managed separately.

## Managing Workspaces

You can create, list, and select workspaces using the `terraform workspace` command:

```bash
terraform workspace new [project-name]  # create new workspace
terraform workspace select [project-name]  # switch to a workspace
terraform workspace list  # list all workspaces
```

When a new workspace is created, a new directory named `terraform.tfstate.d` is created that contains directories for each workspace, each containing their respective `terraform.tfstate` file.

To display the contents of the directory, you can use the `tree` command:

```bash
tree terraform.tfstate.d/
```

## Workspace-Specific Variables

You can use workspace-specific variables to customize your configuration for different workspaces. For example, you might have different regions or AMIs for your dev and prod environments:

```yml
module "payroll_app" {
    source = "../modules/payroll-app"
    app_region = lookup(var.region, terraform.workspace)
    ami = lookup(var.ami, terraform.workspace)
}
```

In the `variables.tf` file, you can define a `map` variable for each environment:

```yml
variable "region" {
    type = map
    default = {
        "us-payroll" = "us-east-1"
        "uk-payroll" = "eu-west-2"
        "india-payroll" = "ap-south-1"
    }
}

variable "ami" {
    type = map
    default = {
        "us-payroll" = "ami-24e140119877avm"
        "uk-payroll" = "ami-35e140119877avm"
        "india-payroll" = "ami-55140119877avm"
    }
}
```

In the `provider.tf` file, you can use the `lookup` function to get the value for the current workspace:

```yml
provider "aws" {
  region                      = lookup(var.region, terraform.workspace)
  skip_credentials_validation = true
  skip_requesting_account_id  = true
  s3_force_path_style = true
  endpoints {
    ec2 = "http://aws:4566"
    dynamodb = "http://aws:4566"
    s3 = "http://aws:4566"
  }
}
```

## Testing Functions

You can use the `terraform console` command to test functions and expressions. For example, to get the current workspace, you can use the `terraform.workspace` variable:

```bash
terraform console
terraform.workspace
```

## Running Terraform with Workspaces

To run Terraform with a specific workspace, you can select the workspace and then run `terraform apply`:

```bash
terraform workspace select [project-name]
terraform apply
```
