**Variable Definition Preference**
1 - env vars
2 - terraform.tfvars
3 - *.auto.tfvars (in alphabetical order)
4 - -var or -var-file (cli flags)

**Basic types**
- string
- number
- bool
- list - can have duplicate values
- map - key-value pairs
- set - can't have duplicate values
- objects
- tuple - can contain different var types
- any


**CLI**
`terraform apply -var "var-name=var-value"` 
`terraform output <var-name>`

**The Variable block**
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

**Examples**
variables.tf
```yml
variable "prefix" {
    default = ["test", "dev", "prod"]
    type = list(string)
}
variable "separator" {
    default = {
        "test" = "_"
        "dev" = "-"
        "prod" = "*"
    }
    type = map(string)
}
variable "length" {
    default = [1, 2, 3]
    type = set(number)
}
variable "person" {
    default = {
        name = "my-name"
        identity = "my-identity"
        age = "1"
    }
    type = object({
        name = string
        identity = string
        age = number
    })
}
variable "web" {
    default = ["web1", 1, "true"]
    type = tuple([string, number, bool])
}
```

#to utilise vars
```yml
resource "random_pet" "test" {
    prefix = var.prefix[0]
    separator = var.separator["test"]
    length = var.length[0]
}
```

**Variables in bulk**
`terraform.tfvars, terraform.tfvars.json`
`*.auto.tfvars, *.auto.tfvars.json`
- these var files are automatically loaded by TF
```yml
var-name="var-value"
...
...
```


**Output Variables**
 - can be used to store value of an expression then feed to other resources
 - output displays after `apply`
main.tf
```yml
resource "aws_instance" "my-instance" {
    ami = var.ami
    instance_type = var.instance)type
}

output "public-ip" {
    value = aws_instance.my-instance.public_ip
    description = "display public IP of instance"
}
```
#to display outputs
`terraform output`
`terraform output public-ip`