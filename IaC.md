# Types of Infrastructure as Code (IaC) Tools

Infrastructure as Code (IaC) is the process of managing and provisioning computer data centers through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools.

## Configuration Management Tools

These tools are designed to install and manage software on existing servers. They maintain a standard structure, provide version control, and are idempotent, meaning they can be applied multiple times without changing the result beyond the initial application. They typically use a procedural approach, defining the steps that need to be executed to achieve the desired state.

- **Ansible**: An open-source software provisioning, configuration management, and application-deployment tool.
- **Puppet**: An automated administrative engine that performs administrative tasks (such as adding users, installing packages, and updating server configurations) based on a centralized specification.
- **SaltStack**: A Python-based, open-source software for event-driven IT automation, remote task execution, and configuration management.

## Server Templating Tools

These tools are used to create images of pre-configured servers. These images, which can be virtual machines or Docker containers, come with all the necessary software and dependencies installed. This approach supports the concept of immutable infrastructure, where servers are not modified after they're deployed.

- **Docker**: An open-source platform that automates the deployment, scaling, and management of applications using container virtualization technology.
- **Packer**: An open-source tool for creating identical machine images for multiple platforms from a single source configuration.
- **Vagrant**: A tool for building and managing virtual machine environments in a single workflow.

## Provisioning Tools

Also known as orchestration tools, these are used to automate the deployment of servers and other infrastructure. They use a declarative approach, where you define the desired state of your infrastructure, and the tool figures out how to achieve that state.

- **Terraform**: An open-source infrastructure as code software tool that provides a consistent CLI workflow for managing a wide variety of service providers.
- **CloudFormation**: A service that helps you model and set up your Amazon Web Services resources so you can spend less time managing those resources and more time focusing on your applications that run in AWS.
