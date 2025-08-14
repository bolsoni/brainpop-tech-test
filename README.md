# Static Website Setup

Static website hosting on AWS with automated deployment via CircleCI.

## Setup Instructions

### 1. Deploy Infrastructure

```bash
terraform init
terraform plan
terraform apply
```

Note the outputs after deployment:
- S3 bucket name: `brainpop-techtest-static`
- CloudFront distribution ID (needed for CircleCI)

### 2. Configure CircleCI

Create a context called `aws-static-website` with these environment variables:

```
AWS_ACCESS_KEY_ID=<aws-access-key>
AWS_SECRET_ACCESS_KEY=<aws-secret-key>
AWS_DEFAULT_REGION=us-east-1
AWS_S3_BUCKET_NAME=brainpop-techtest-static
AWS_CLOUDFRONT_DISTRIBUTION_ID=<from-terraform-output>
```

Get the CloudFront distribution ID:
```bash
terraform output cloudfront_distribution_id
```

### 3. Repository Structure

```
brainpop-tech-test/
├── .circleci/config.yml
├── index.html
└── main.tf
```

### 4. Deploy

Push `index.html` to the `main` branch. CircleCI will automatically deploy it to:
https://techtest.leonardobolsoni.com

## Daily Usage

1. Edit `index.html`
2. Push to `main` branch
3. Changes go live automatically
