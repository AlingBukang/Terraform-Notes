# Modules in Terraform

Modules in Terraform are self-contained packages of Terraform configurations that are managed as a group. Modules are used to create reusable components, improve organization, and to treat pieces of infrastructure as a single entity.

A module allows you to group resources together and reuse this group later. It creates logical abstraction on the top of some resource set.

Any Terraform configuration file (.tf) in a directory forms a module.

Pros:

- simpler config files
- lower risk
- reusable

## Using Modules

Modules can be called from other Terraform files using the `module` block:

**Local module**
`main.tf`
```yml
module "dev-webserver" {
    source = "../dir/module"
}
```

**Terreform module**
`main.tf`
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

## Module Structure

A typical module consists of the following files:

`main.tf`: This is the main file that contains the resources that will be created.

`variables.tf`: This file defines any input variables for the module.

`outputs.tf`: This file defines any output variables for the module.

`README.md`: This file contains documentation for the module.

## Module Sources

Modules can be loaded from a variety of sources:

- Local paths
- GitHub
- Bitbucket
- Generic git, Mercurial repositories
- HTTP URLs
- S3 buckets
- GCS buckets

## Module Versions

You can specify a specific version of a module to use:

```yml
module "consul" {
    source = "hashicorp/consul/aws"
    version = "0.0.5"
    servers = 5
}
```
