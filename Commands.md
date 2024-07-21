# Terraform Commands

## Initialization and Planning

- `terraform init`: Initializes your Terraform working directory. This will download and install the necessary plugins for your configuration.
- `terraform plan`: Generates an execution plan. This is a "dry run" that shows you what changes Terraform will make without actually applying them.

## Applying and Destroying

- `terraform apply [-auto-approve] [-refresh=false] [-var "var-name=var-value"]`: Applies the changes required to reach the desired state of the configuration. You can use various flags to customize the behavior.

## Validation and Formatting

- `terraform validate`: Validates the configuration files for syntax and internal consistency.
- `terraform fmt`: Rewrites configuration files in a canonical format and style.

## Inspection

- `terraform show [-json]`: Provides a human-readable output from a state or plan file. Use `-json` to get machine-readable output.
- `terraform output [var-name]`: Displays the outputs of your infrastructure. If an output name is specified, only the value of that output is printed.

## State Management

- `terraform refresh`: Updates the state file of your infrastructure with metadata from the actual resources.
- `terraform state [list|mv|pull|rm|show] [opts] [args]`: Advanced state management. Be careful, as improper use can corrupt your state file.

## Workspace Management

- `terraform workspace new [project-name]`: Creates a new workspace.
- `terraform workspace list`: Lists all existing workspaces.
- `terraform workspace select [project-name]`: Switches to another workspace.

## Other Commands

- `terraform providers`: Displays information about the provider requirements of the current configuration.
- `terraform graph`: Generates a visual representation of the dependencies in your configuration.
- `terraform version`: Displays the version of Terraform and any provider plugins in use.
- `terraform taint`: Marks a resource as tainted, forcing it to be destroyed and recreated on the next apply.
- `terraform import`: Imports existing infrastructure into your Terraform state.
- `terraform get`: Downloads and installs modules needed for the configuration.
- `terraform console`: Provides an interactive console for evaluating expressions.

Remember to always check the official Terraform documentation for the most up-to-date and detailed information.
