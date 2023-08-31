Used to run tasks or command on local or remote resources.

**Pass an inline script with remote exec**
```yml
resource '"aws_instance" "webserver" {
    ami = "ami-xxxx"
    instance_type = "t2.micro"
    provisioner "remote-exec" {
        inline = [ "sudo apt update",
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

**local exec**
```yml
resource '"aws_instance" "webserver" {
    ami = "ami-xxxx"
    instance_type = "t2.micro"
    provisioner "local-exec" {
        when = destroy
        command = "echo ${whoami}"
    }
}
```