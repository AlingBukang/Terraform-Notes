**Commands:**
`terraform init` - checks all config files in the current dir; download, install and initialise plugins 
`terraform plan` - generates execution plan/blueprint; dry run
`terraform apply [-auto-approve] [-refresh=false] [-var "var-name=var-value"`] - creates resources

`terraform validate` - to verify is config is valid
`terraform fmt` - formats config files on the current dir into a canonical format to improve readability
`terraform show [-json]` - prints the current state of the infrastructure
`terraform destroy -y`
`terraform output [var-name]` - to print out output variables
`terraform refresh` - syncs TF with real-world infrastructure; this will only modify the state file and not the infrastructure
`terraform providers` - to show info about provider requirements of the config on the current dir
`terraform providers mirror /root/terraform/<new_local_file>`
`terraform graph` - creates a visual representation of dependencies in a TF config
`terraform version` - to list installed plugins and TF versions

`terraform state [list|mv|pull|rm|show] [opts] [args]`

`terraform taint`
`terraform import`
`terraform get`
`terraform console` - use for functions

`terraform workspace new [project-name]`
`terraform workspace list`
`terrform workspace select [project-name]`  - to switch tf projects

