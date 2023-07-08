# Host a static web page on S3 using GitHub Actions

- GitHub Actions
- Identity and Access Management (IAM) for creating Service Role
- S3
  
![pro1](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/ad86ab4a-a305-47ea-a5a9-7e6b0216b44a)

```
name: Portfolio Deployment

on:
  push:
    branches:
    - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v1

    - name: Configure AWS Credentials
      uses: aws-actions/configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: us-east-1

    - name: Deploy static site to S3 bucket
      run: aws s3 sync . s3://portfolio-aws-github-action --delete

```
![git act](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/2adfb326-f353-4caf-9307-d140d1117fcb)

![actions ss](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/fef1913b-2767-4878-a44f-3fc84761c86f)


```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::portfolio-aws-github-action/*"
        }
    ]
}
```
![s3 bucket ss](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/a08bb42c-5d31-4401-8e5f-f9fdc0d2057b)

![portfolio](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/28ff6e68-e3c0-493f-a382-693ee6611cae)

# [Click Me :)](http://portfolio-aws-github-action.s3-website.ap-south-1.amazonaws.com/)
