A module allows you to group resources together and reuse this group later. It creates logical abstraction on the top of some resource set.

Any Terraform configuration file (.tf) in a directory forms a module.

Pros:
- simpler config files
- lower risk
- reusable

**Local module**
main.tf
```yml
module "dev-webserver" {
    source = "../dir/module"
}
```

**Terreform module**
main.tf
```yml
module "security_group_ssh" {
    source = "terraform-aws-modules/security-group/aws/modules/ssh"
    version = "3.16.0"
    # required arguments here
    vpc_id = "vpc-xxxx"
    ingress_cidr_blocks = ["10.x.x.x/16"]
    name = "ssh-access"
}
```
