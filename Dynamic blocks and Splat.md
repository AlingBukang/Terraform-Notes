# Dynamic Blocks and Splat Expressions in Terraform

## Dynamic Blocks

Dynamic blocks in Terraform allow us to create blocks dynamically based on a complex type value. In the below example, we're creating multiple `ingress` blocks in the `aws_security_group` resource based on the `ingress_ports` variable.

`main.tf`

```yml
resource "aws_vpc" "backend-vpc" {
    cidr_block = "10.0.0.0/16"
    
    tags = {
        name = "backend-vpc"
    }
}

resource "aws_subnet" "private-subnet" {
    vpc_id = aws_vpc.backend-vpc.id
    cidr_block = "10.0.2.0/24"

    tags = {
        name = "private-subnet"
    }
}

resource "aws_security_group" "backend-sg" {
    name = "backend-sg"
    vpc_id = aws_vpc.backend-vpc.id

    dynamic "ingress" {
        iterator = port
        for_each = var.ingress_ports
        content {
            from_port =  port.value
            to_port =  port.value
            protocol = "tcp"
            cidr_blocks = ["0.0.0.0/0"]
        } 
    }
}
```

The `iterator` argument(_optional_) is used to define a name for the local variable that will represent each element of the complex value. If omitted, the name of the attribute itself is used.

## Splat Expressions

Splat expressions in Terraform allow us to access attributes across all elements of a list or set. In this example, we’re using a splat expression to get the `to_port` attribute of all `ingress` blocks in the `aws_security_group` resource.

`variables.tf`

```yml
variable "ingress_ports" {
    type = list(number)
    default = [22, 8080]
}

output "to_ports" {
    value = aws_security_group.backend-sg.ingress[*].to_port
}
```

The [*] is the splat operator, and it’s used to get a list of attribute values from all elements in the list or set.
