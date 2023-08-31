**Data source**
```yml
data "local_file" "pet" {
    filename = "/dir/file"
}
#To reference data source:
resource "local_file" "dog" {
    filename = "/dir/file"
    content = data.local_file.dog.content
}
```

**Data source with filter**
```yml
data "aws_key_pair" "ec2-key" {
    filter {
        name = "tag:env"
        values = ["test"]
    }
}
#To reference data source:
resource "aws_instance" "ec2-test" {
    ami = var.ami
    instance_type = var.instance_type
    key_name = data.aws_key_pair.ec2-key.key-name
}
```