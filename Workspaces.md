**Workspace**
- use for multi-environment set-up, e.g. dev, prod
  
`terraform workspace list` 
`terraform workspace new [project-name]` - create new workspace
`terrform workspace select [project-name]`  - to switch tf projects

A new directory called `terraform.tfstate.d` will be created that will contain dirs of each workspaces containing their respective `terraform.tfstate` file.

To display contents of the dir:
`tree terraform.tfstate.d/`

**main.tf**
```yml
module "payroll_app" {
    source = "../modules/payroll-app"
    app_region = lookup(var.region, terraform.workspace)
    ami = lookup(var.ami, terraform.workspace)
}
```

**variables.tf**
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

**provider.tf**
```yml
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "4.15.0"
    }
  }
}

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

**To test functions**
Use `terraform console`
`terraform.workspace`

**To run**
`terraform workspace select [project-name]; terraform apply`