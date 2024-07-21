# Terraform Basics

Terraform is an open-source infrastructure as code software tool that allows you to define and provide data center infrastructure using a declarative configuration language.

## Main Terraform Files

A typical Terraform project consists of the following files:

- `terraform.tf`: This is the main configuration file where you define your infrastructure.
- `main.tf`: This file usually contains the actual cloud resources declarations.
- `variables.tf`: This file is used to declare variables.
- `outputs.tf`: This file is used to declare outputs.
- `provider.tf`: This file is used to specify and configure the providers.

## Understanding a Terraform Configuration File

A Terraform configuration file has several parts:

- Block name: This is the type of the block. For example, `resource`.
- Resource type: This is the type of resource to create. For example, `aws_instance`.
- Resource name: This is a name used to refer to this resource in the configuration.
- Arguments: These are key-value pairs that configure the behavior of the resource.

Here's an example:

```yml
# This is a resource block, which creates a local file
resource "local_file" "games" {
  # The file argument specifies the path of the file
  file     = "/root/favorite-games"
  # The content argument specifies the content of the file
  content  = "FIFA 21"
}
```

### Depends_on

The `depends_on` argument is used to handle dependencies that Terraform can't automatically infer. This is useful when a resource depends on another resource's state or configuration.

```yml
depends_on = [
    resource.name
]
```

### Lifecycle Rules

Lifecycle rules are used to manage the lifecycle of a resource. They can help prevent accidental deletion of resources and manage updates to resources.

`create_before_destroy`: This rule ensures that the new resource is created before the old one is destroyed during an update. This is useful when you want to minimize downtime during updates.

`prevent_destroy`: This rule prevents the resource from being destroyed. This is useful when you want to protect critical resources from accidental deletion.

`ignore_changes`: This rule can be used to ignore changes to certain attributes of a resource. This is useful when you want to prevent Terraform from recreating a resource due to changes to an attribute that doesn’t affect the resource’s functionality.

`main.tf`

```yml
resource "" "" {
    ....
    lifecycle {
    create_before_destroy = true
    }
}
```

### Version Constraints

Version constraints are used to specify the required versions of Terraform and its providers. This is useful to ensure that your configuration is compatible with the versions of Terraform and providers you are using.

`provider.tf`

```yml
terraform {
    required_providers {
        local = {
            source = "hashicorp/local"
            version = "~> 1.4.0"
        }
    }
}
```

### Log Levels

Terraform uses different log levels to provide more or less verbose logging information. This is useful for debugging your Terraform configurations.

- info
- warning
- error
- debug
- trace

You can set the log level using the `TF_LOG` environment variable:

```yml
export TF_LOG=TRACE
export TF_LOG_PATH=/tmp/terraform.log
```

#### Aliases

Aliases are used to create multiple configurations for the same provider. This is useful when you want to manage resources in different regions with the same provider.

`provider.tf`

```yml
provider "aws" {
    region = "ca-central-1"
    alias = "central"
}
```

To use an alias, you specify it in the `provider` argument of a resource:

```yml
resource "aws_key_pair" "test" {
    key_name = "test"
    public_key = "pk here"
    provider = aws.central
}
```

### Output

Outputs are like return values for a Terraform module. You can use them to expose a subset of a module’s resource attributes to a user, or to pass information between modules.

`outputs.tf`

```yml
output "name" {
    value = data.local_file.content
}
```
