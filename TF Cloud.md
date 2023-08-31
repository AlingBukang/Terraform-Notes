**AWS IAM with TF**
```yml
provider "aws" {
    region = "us-west-2"
}

resource "aws_iam_user" "name" {
    name = "username"
    tags = {
        Description = "Description"
    }
}

resource "aws_iam_policy" "admin" {
    name = "admin"
    policy = <<EOF
    {
        "Statement" : [
            {
                "Effect": "Allow",
                "Action": "",
                "Resource": ""
            }
        ]
    }
    EOF
}

resource "aws_iam_user_policy_attachment" "admin" {
    user = aws_iam_user.admin.name
    policy_arn = aws_iam_policy.admin.arn
}
```


