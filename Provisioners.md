# Terraform Provisioners

Provisioners in Terraform can be used to model specific actions on the local machine or on a remote machine in order to prepare servers or other infrastructure objects for service.

## Remote-Exec Provisioner

The `remote-exec` provisioner invokes a script on a remote resource after it is created. This can be used to run a configuration management tool, bootstrap into a cluster, etc. 

Here's an example of how to use the `remote-exec` provisioner to `install and start nginx` on an AWS `instance`:

```yml
resource "aws_instance" "webserver" {
    ami = "ami-xxxx"
    instance_type = "t2.micro"
    provisioner "remote-exec" {
        inline = [ 
            "sudo apt update",
            "sudo apt install nginx -y",
            "sudo systemctl enable nginx",
            "sudo systemctl start nginx",
        ]
    }
    connection {
        type = "ssh"
        host = self.public_ip
        user = "username"
        private_key = file("/dir/.ssh")
    }
    key_name = aws_key_pair.web.id
    vpc_security_group_ids = [ aws_security_group.ssh-access.id ]
}
```

## Local-Exec Provisioner

The `local-exec` provisioner invokes a local executable after a resource is created. This invokes a process on the machine running Terraform, not on the resource.

Here’s an example of how to use the `local-exec provisioner` to execute a command locally when an AWS instance is destroyed:

```yml
resource "aws_instance" "webserver" {
    ami = "ami-xxxx"
    instance_type = "t2.micro"
    provisioner "local-exec" {
        when = destroy
        command = "echo ${whoami}"
    }
}
```
