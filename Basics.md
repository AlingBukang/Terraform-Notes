**Main TF files:**
terraform.tf
main.tf
variables.tf
outputs.tf
provider.tf


**Main parts of a TF config file**
- block name
- resource type
- resource name
- arguments

Ex.
```yml
resource "local_file" "games" {
  file     = "/root/favorite-games"
  content  = "FIFA 21"
}
```
block name = resource
provider/plugin name - local
resource type - local_file
resource name - games
arguments - file, content


**Depends_on**
```yml
depends_on = [
    resource.name
]
```

**Lifecycle rules**
- create_before_destroy
- prevent_destroy
- ignore_changes = all or []

main.tf
```yml
resource "" "" {
    ....
    lifecycle {
    create_before_destroy = true
    }
}
```

**Version constraints:**
provider.tf
```yml
terraform {
    required_providers {
        local = {
            source = "hashicorp/local"
            version = "~> 1.4.0"
        }
    }
}
```

**Log Levels**
info, warning error, debug, trace
```yml
export TF_LOG=TRACE
export TF_LOG_PATH=/tmp/terraform.log
```

**Aliases**
provider.tf
```yml
provider "aws" {
    region = "ca-central-1"
    alias = "central"
}
```
#to utilise alias
```yml
resource "aws_key_pair" "test" {
    key_name = "test"
    public_key = "pk here"
    provider = aws.central
}
```

**Output:**
outputs.tf
```yml
output "name" {
    value = data.local_file.content
}
```