`terraform state [list|mv|pull|push|rm|show] [opts] [args]`

**with json query**
```sh
terraform state pull | jq '.resources[] | select(.name == "state-locking-
db")|.instances[].attributes.hash_key'`
```

**Local State**

When a resource is created after running the `terraform apply` command, a state file is created within the dir where the config file are located, by default.

`terraform.tfstate` - state file
`terraform.tfstate.backup` - backup

The state file contains the complete record of the infrastructure(blueprint) created by TF. It is the single source-of-truth for TF when executing commands such as `plan` and `apply`.

Running `plan` or `plan` on an existing resources, TF will detect difference between the planned config and existing resources and will take note of the changes to be applied. The TF state will be refreshed in-memory prior to plan or apply. The refreshed state will be used to calculate the plan, but will not be persisted to local or remote state storage.

**To force TF not to refresh state**
`terraform apply -refresh=false`


**Remote State**
- allows collaboration
- central manage
- implements state locking to safeguard from users using the same state file at the same time
- security - can implement encryption of state file and state locking

Best practice - implement state locking by storing TF state into a remote state backend such as file sharing like S3, TF cloud, etc. instead of version control.

Remote State Backend providers:
- AWS S3
- Google Cloud Storage
- HashiCorp Consul
- Terraform Cloud

Consul and TF Cloud automatically load and upload state files.

**Implement remote state locking with S3 and DynamoDB**

main.tf
```yml
resource "local_file" "pet" {
    filename = "/root/pets/txt"
    content = "List of pets"
}
```

terraform.tf
```yml
terraform {
    backend "s3" {
        bucket = "unique-bucket-name"
        key = "test/terraform.tfstate"
        region = "us-west-1"
        dynamodb_table = "state-locking"
    }
}
```