# Terraform Variables and Outputs

## Variable Definition Preference

Terraform has several ways to define variables, and they have the following order of precedence:

1. Environment variables (env vars)
2. `terraform.tfvars` file, if present
3. `*.auto.tfvars` files, if present, in alphabetical order
4. `-var` and `-var-file` options on the command line (cli flags)

## Basic Types

Terraform supports several types of variables:

- `string`
- `number`
- `bool`
- `list`: Can have duplicate values
- `map`: Key-value pairs
- `set`: Can't have duplicate values
- `object`: A collection of named attributes with specific types
- `tuple`: A sequence of types
- `any`: Any type is acceptable

## The Variable Block

You can define a variable in Terraform using the `variable` block. You can specify the `type`, `default value`, and a `description`. You can also add a `validation condition`.

```yml
variable "ami" {
    default = "default value should be consistent with var type"
    type = string
    description = "Description here"
    validation {
        condition = substr(var.ami, 0, 4) == "ami-"
        error_message = "The ami should start with \"ami-\"."
    }
}
```

### Variables in Bulk

You can define multiple variables at once in a `terraform.tfvars` or `*.auto.tfvars` file. These files are automatically loaded by Terraform.

```yml
var-name="var-value"
...
...
```

# Output Variables

Output variables are a way to tell Terraform what data is important. This data is outputted when `apply` is called, and can be queried using the `terraform output` command.

```yml
output "public-ip" {
    value = aws_instance.my-instance.public_ip
    description = "display public IP of instance"
}
```

To display outputs:

```bash
terraform output
terraform output public-ip
```
