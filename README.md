# Host a static web page on S3 using GitHub Actions (Test)

## [GitHub Actions](https://docs.github.com/en/actions):
  Automate, customize and execute your software development workflows in your repository with GitHub Actions. You can discover, create, and share actions to perform any job you'd like, including CI/CD, and combine actions in a customized workflow.
  

- GitHub Actions
- Identity and Access Management (IAM) for creating Service Role
- Amazon S3
  
## Simple Project Architecture

![pro1](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/ad86ab4a-a305-47ea-a5a9-7e6b0216b44a)

## Step 1: Setup a project
1. Create a repository
2. Clone the repository on the local IDE
3. Create a html file a write simple content.
4. Folder structure like this
![vs code](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/689b52c1-1872-4811-ae08-ee20fb84f0ab)
5. Push this code on the GitHub repository.
6. Create a S3 Bucket
![s3](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/7ad5086a-9df5-44e2-9631-65dd44377bed)
7. Gives all public assecc.
8. Go to the properties in the bucket -> Static website hosting -> Click Edit -> Enable
9. Go to the permissions section in the bucket -> Bucket policy -> Edit -> Add this policy

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
## Step 2: Setup a Workflow

1. Go to your GitHub repository
2. Click on Actions
   ![actions](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/fa03f769-2451-4345-ab95-093bc782519b)
3. Click on `set up a workflow yourself`
   ![setup workflow](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/fc5ca3b2-1681-471c-ac0f-50b2f55f132d)

After looking like this `(repo_name)/.github/workflows/main.yml`

- Write a workflow in `main.yml`
  
```
name: Deployment

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
- [Reference for creating this file](https://github.com/actions)
- [Reference for creating this file](https://github.com/actions/checkout)

## Step 3: Setup your AWS Credentials

1. Go to the repository Settings
2. Click on `secrets and variables` -> `Actions`
   ![sec](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/b4cd8997-c1f8-4548-81bf-8e8800093bab)
3. After Click on New repository secret -> Name* `AWS_ACCESS_KEY_ID` -> Secret* `Add AWS IAM user `Access key`
4. One's again click on New repository secret -> Name* `AWS_SECRET_ACCESS_KEY` -> Secret* `Add AWS IAM user `Secret access key`

- After Committing this all changes and see this.
      
![git act](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/2adfb326-f353-4caf-9307-d140d1117fcb)

![actions ss](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/fef1913b-2767-4878-a44f-3fc84761c86f)

![s3 bucket ss](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/a08bb42c-5d31-4401-8e5f-f9fdc0d2057b)

![portfolio](https://github.com/darjidhruv26/Portfolio_AWS_GitHub_action/assets/90086813/28ff6e68-e3c0-493f-a382-693ee6611cae)

#                            [Click Me :)](http://portfolio-aws-github-action.s3-website.ap-south-1.amazonaws.com/)
