# AWS IAM CloudFormation

This repository contains CloudFormation templates for creating IAM service roles for Lambda and S3, following AWS best practices. It also includes GitHub Actions workflows to deploy the CloudFormation stacks to AWS.

## Contents

- `cloudformation/iam-roles.yml`: CloudFormation template for IAM roles and policies
- `.github/workflows/deploy-cloudformation.yml`: GitHub Actions workflow for deployment

## IAM Resources Created

The CloudFormation template creates the following resources:

1. **S3 Access Role**: A role for S3 service with appropriate permissions
2. **Lambda Execution Role**: A role for Lambda functions with logging and S3 access
3. **S3 Access Policy**: A managed policy with least privilege S3 permissions
4. **Lambda Basic Execution Policy**: A managed policy for basic Lambda execution (CloudWatch Logs)
5. **Lambda S3 Access Policy**: A managed policy for Lambda to access S3 with least privilege

## Setup Instructions

### Prerequisites

- AWS Account
- GitHub Account
- Permissions to create IAM resources in your AWS account

### Configuration

1. Fork or clone this repository
2. Add the following GitHub repository secrets:
   - `AWS_ACCESS_KEY_ID`: Your AWS access key ID
   - `AWS_SECRET_ACCESS_KEY`: Your AWS secret access key
   - `AWS_REGION`: The AWS region to deploy resources (e.g., `us-east-1`)

### Deployment

You can deploy the CloudFormation stack in two ways:

1. **Automatic deployment**: Push changes to the `main` branch, which will automatically trigger the workflow if there are changes in the `cloudformation` directory.

2. **Manual deployment**: Use the GitHub Actions workflow dispatch feature:
   - Go to the Actions tab in your repository
   - Select the "Deploy CloudFormation Stack" workflow
   - Click "Run workflow"
   - Input your desired parameters:
     - Environment: `dev`, `test`, or `prod`
     - Project name: A name for your project (used in resource naming)

## Customization

You can customize the IAM policies in the CloudFormation template (`cloudformation/iam-roles.yml`) to match your specific requirements. Just ensure you follow the principle of least privilege.

## Best Practices Implemented

- **Least Privilege**: Only necessary permissions are granted
- **Resource-Level Permissions**: Resources are scoped to specific project and environment
- **Condition Keys**: Where appropriate, conditions limit when permissions are granted
- **Managed Policies**: Permissions are organized into reusable managed policies
- **Naming Conventions**: Consistent naming with project and environment variables
- **Tagging**: Resources are tagged with project and environment information

## Outputs

The CloudFormation stack outputs the ARNs of all created roles and policies, which can be used in other CloudFormation templates via cross-stack references.
