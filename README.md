# nhk-terraform-state

Amazon S3 bucket and DynamoDB table for storing Terraform state.

## Overview

From the Terraform documentation on [S3 backends](https://www.terraform.io/language/settings/backends/s3)...

>Stores the state as a given key in a given bucket on [Amazon S3](https://aws.amazon.com/s3). This backend also supports state locking and consistency checking via [DynamoDB](https://aws.amazon.com/dynamodb), which can be enabled by setting the `dynamodb_table` field to an existing DynamoDB table name.

## Usage

```hcl
terraform {
  backend "s3" {
    bucket         = "nhk-terraform-state"
    key            = "<path/to/key>"
    region         = "us-east-1"
    dynamodb_table = "nhk-terraform-state"
  }
}
```

## Development

### Validation

```bash
aws cloudformation validate-template \
  --template-body file://template.yaml
```

### Deployment

```bash
STACK_NAME=$(basename "$(pwd)")
```

```bash
aws cloudformation deploy \
  --stack-name "${STACK_NAME}" \
  --template template.yaml
```
