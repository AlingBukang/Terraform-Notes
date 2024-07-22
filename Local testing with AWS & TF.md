## Mock AWS for local testing using Terraform

`provider.tf`

```yml
provider "aws" {
  region                      = "us-east-1"
  skip_credentials_validation = true
  skip_requesting_account_id  = true

  endpoints {
    iam                       = "http://aws:4566"
  }
}
```

In this configuration, we’re setting up the AWS provider to interact with a local endpoint (`http://aws:4566`) for the IAM service. This can be useful when we’re developing or testing Terraform configurations and we don’t want to make changes to real AWS resources.

- `region`: This is the AWS region where the resources would be created. In this case, it’s set to `us-east-1`.
- `skip_credentials_validation`: This is set to true to skip validation of the provided AWS credentials. This is useful when mocking AWS as the mock service won’t be able to validate real AWS credentials.
- `skip_requesting_account_id`: This is set to true to prevent Terraform from requesting the account ID from AWS. This is necessary when mocking AWS as the mock service won’t have a real AWS account ID.
- `endpoints`: This is where we specify the service-specific endpoint URLs. In this case, we’re setting the IAM service endpoint to the mock service URL (http://aws:4566).

Remember, this configuration assumes that we have a mock AWS service running locally at http://aws:4566. There are several tools available that can help run a mock AWS service, such as LocalStack.
