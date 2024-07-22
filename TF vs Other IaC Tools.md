# Terraform vs Other IaC Tools

## Terraform vs CloudFormation

- **`CloudFormation`** is a service offered by `AWS` for infrastructure provisioning. It's tightly integrated with AWS services but lacks support for other cloud providers. It uses `JSON or YAML` for its configuration language.

- **`Terraform`** is a tool that works with multiple cloud providers, including AWS, Azure, Google Cloud, and many others. It uses its own configuration language, `HCL`, which is more human-readable compared to `JSON` or `YAML`.

## Terraform vs Ansible

- **`Ansible`** is primarily a configuration management tool that can also do infrastructure provisioning. It's imperative, meaning you need to specify the sequence of tasks to reach the desired state. It uses `YAML` for its configuration language and is agentless, requiring only SSH and Python on the managed systems.

- **`Terraform`** is a `declarative` infrastructure provisioning tool, meaning you only need to specify the desired state and Terraform figures out how to achieve it. It uses `HCL` for its configuration language.

## Terraform vs Pulumi

- **`Pulumi`** is similar to Terraform in that it's a multi-cloud infrastructure provisioning tool. However, Pulumi uses standard programming languages like `JavaScript`, `TypeScript`, `Python`, `Go`, and `.NET` instead of a `custom DSL`.

- **Terraform** uses its own `DSL`, `HCL`, which might have a steeper learning curve compared to standard programming languages but provides a consistent way to describe your infrastructure.

## Terraform vs Chef

- **`Chef`** is a configuration management tool that uses `Ruby` as its configuration language. It requires a `Chef server` to communicate with the managed systems and uses a `pull-based approach`, where the managed systems pull their configuration from the Chef server.

- **`Terraform`** is a provisioning tool and doesn't handle configuration management. It directly communicates with the cloud provider's API to create, modify, or destroy resources.

## Terraform vs Puppet

- **`Puppet`** is a configuration management tool that uses its own `declarative language` to describe system configuration. It uses a `master-agent model`, where the managed systems pull their configuration from the `Puppet master`.

- **`Terraform`** is a `provisioning tool` and doesn't handle configuration management. It directly communicates with the cloud provider's API to create, modify, or destroy resources.

## Terraform vs SaltStack

- **`SaltStack`** is a `configuration management and orchestration tool` that uses `YAM`L in conjunction with the `Jinja2 templating engine` for its configuration language. It can use both a `master-agent` and an `agentless mode`.

- **`Terraform`** is a provisioning tool and doesn't handle configuration management. It directly communicates with the cloud provider's API to create, modify, or destroy resources.
