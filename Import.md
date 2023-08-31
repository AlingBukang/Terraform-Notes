**Import existing resources into TF**
Import command doesn't update the config file. only state file is updated on successful import.

_Example:_ import an existing EC2 instance
main.tf
```yml
resource "aws_instance" "webserver-2" {
    ami = "ami-xxx"
    instance_type = "t2.micro"
    key_name = "ws"
    vpc_securitu_group_ids = ["sg-xxx"]
}
```

_Run Import Command:_
`terraform import aws_instance.webserver-2 <id-of-ec2-to-import>`

_Then Plan & Apply:_
`terraform plan`
`terraform apply`

