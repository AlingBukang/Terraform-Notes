# Terraform State

In Terraform, the "state" is a crucial component that keeps track of the resources it manages. After creating resources, Terraform saves a JSON-formatted map of the resources in the `terraform.tfstate` file.

## Local State

By default, Terraform stores the state locally in a file named `terraform.tfstate`. When running `terraform plan` or `terraform apply`, Terraform will detect the difference between the last-known state and the current state. To force Terraform not to refresh the state, you can use the `-refresh=false` option.

```bash
terraform apply -refresh=false
```

## Remote State

For team-based workflows, it is recommended to use a `shared remote state`. This allows for better collaboration and prevents any conflicts in the state. Remote state is stored on a remote data store (like AWS S3, GCS, etc.) and includes features like state locking and encryption.

Here’s an example of how to configure Terraform to store the state in an S3 bucket and use a DynamoDB table for state locking:

`main.tf`
```yml
resource "local_file" "pet" {
    filename = "/root/pets/txt"
    content = "List of pets"
}
```

`terraform.tf`
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

## Terraform State Commands

Terraform provides several commands to manage and inspect the state:

- `terraform state list`: List resources in the state.
- `terraform state mv`: Move an item in the state.
- `terraform state pull`: Manually download and output the state from remote state.
- `terraform state push`: Manually upload a local state file to remote state.
- `terraform state rm`: Remove items from the state.
- `terraform state show`: Show a resource in the state.

You can also use `jq` to query the state in JSON format:

```bash
terraform state pull | jq '.resources[] | select(.name == "state-locking-db")|.instances[].attributes.hash_key'
```
