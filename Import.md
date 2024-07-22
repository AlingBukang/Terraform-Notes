# Importing Existing Resources into Terraform

Terraform is able to import existing infrastructure. This allows you take resources you've created by some other means and bring it under Terraform management. It's important to know that the `terraform import` command does not generate configuration. It only updates the state file.

## Example: Import an Existing EC2 Instance

Let's say you have an existing `EC2` instance that you want to manage with Terraform. You would first add a corresponding resource block to your configuration, like so:

```yml
resource "aws_instance" "webserver-2" {
    ami = "ami-xxx"
    instance_type = "t2.micro"
    key_name = "ws"
    vpc_security_group_ids = ["sg-xxx"]
}
```

Then, you would run the terraform `import command`, replacing `<id-of-ec2-to-import>` with the actual ID of the EC2 instance you want to import:

```bash
terraform import aws_instance.webserver-2 <id-of-ec2-to-import>
```

This will update the Terraform `state file` to include the EC2 instance. However, it does not generate or change the Terraform configuration. Therefore, you must manually write the resource configuration block for the resource, as shown above.

Finally, you can run `terraform plan` to ensure the state matches your configuration, and `terraform apply` to update the infrastructure as needed:

```bash
terraform plan
terraform apply
```
