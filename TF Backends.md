# Terraform Backends

In Terraform, "backends" are responsible for storing state and providing an API for state locking. There are two types of backends: local and remote.

## Local Backend

The local backend stores state on the local filesystem, locks that state with system APIs, and performs operations locally.

## Remote Backend

Remote backends store state remotely and need to be set up with the specific details of your remote storage. They also provide collaboration features and can be categorized into standard and enhanced.

- **Standard Remote Backends**: These backends store the state and provide state locking & consistency checking.
- **Enhanced Remote Backends**: These backends provide the same features as standard backends, with additional features like remote operations.

## Backend Types

Terraform supports a variety of backend types for different remote storage services:

- **Artifactory**: JFrog Artifactory, a universal artifact repository manager.
- **AzureRM**: Azure Resource Manager, for use with Microsoft Azure.
- **Consul**: HashiCorp Consul, a tool for service discovery and configuration.
- **Etcd / Etcdv3**: etcd, a distributed key-value store.
- **GCS**: Google Cloud Storage, for use with Google Cloud.
- **HTTP**: A generic HTTP backend.
- **Manta**: Joyent's Manta, an HTTP-based object store.
- **OSS**: Alibaba Cloud Object Storage Service, for use with Alibaba Cloud.
- **Pg**: PostgreSQL database.
- **S3**: Amazon S3, for use with AWS.
- **Swift**: OpenStack Swift, an open-source cloud storage system.
