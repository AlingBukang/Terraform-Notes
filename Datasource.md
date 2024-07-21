# Data Sources in Terraform

Data sources allow data to be fetched or computed for use elsewhere in Terraform configuration. Use of data sources allows a Terraform configuration to make use of information defined outside of Terraform, or defined by another separate Terraform configuration.

## Local File Data Source

This data source reads the contents of a file into the Terraform state, for use elsewhere in the configuration.

```yml
data "local_file" "pet" {
    filename = "/dir/file"
}
```

To reference this data source in another resource:

```yml
resource "local_file" "dog" {
    filename = "/dir/file"
    content = data.local_file.pet.content
}
```

### AWS Key Pair Data Source with Filter

This data source provides details about a specific key pair within AWS. It can be useful when you want to use an existing key pair while creating AWS resources.


```
data "aws_key_pair" "ec2-key" {
    filter {
        name = "tag:env"
        values = ["test"]
    }
}
```

To reference this data source in another resource:

```
resource "aws_instance" "ec2-test" {
    ami = var.ami
    instance_type = var.instance_type
    key_name = data.aws_key_pair.ec2-key.key_name
}
```

Remember, the `filter` block is used to filter resources based on tags or other attributes. In this case, it’s filtering key pairs that have a tag `env` with the value `test`.
