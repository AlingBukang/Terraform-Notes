**Dynamic Blocks and Splat Expressions**
main.tf
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


variables.tf
```yml
variable "ingress_ports" {
    type = list(number)
    default = [22, 8080]
}

output "to_ports" {
    value = aws_security_group.backend-sg.ingress[*].to_port
}
```