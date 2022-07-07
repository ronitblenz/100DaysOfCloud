![placeholder image](https://miro.medium.com/max/1200/1*bImkauctDDwzT5bOa51MEQ.png)

# Unit Testing and CI/CD using GitHub Actions

## Introduction

What is [CI/CD](https://www.redhat.com/en/topics/devops/what-is-ci-cd)?
- CI --> Continuous Integration
- CD --> Continuous Deployment

Here, we will setup the CI/CD using GitHub Actions and deploy infrastructure on AWS

## Use Case

- Deployment
- Automation


## Cloud Research

Here are the steps for Setting up GitHub Actions for CI/CD :

 - Check the previous day documentations for the steps done till now regarding IAM, S3, CloudFormation, CloudFront, Certificate Manager, API GateWay and DynamoDB
 
 - Create a ```.github``` directory and inside that, create ```workflows``` directory
 - Create ```main.yaml``` inside the above directory and use the following snippet:<br>
 (This configuration includes testing, build and deployment automations and Please make changes according to your naming conventions)

 ```
name: main
on: push
env:
  GO_VERSION: 1.18.3
  
jobs: 
  build-infra:
    runs-on: ubuntu-latest
    timeout-minutes: 2
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-go@v2.1.3
        with:
          go-version: ${{ env.GO_VERSION }}
      - name: test get-function
        run: cd get-function && go test -v ./ && cd ../../
      - name: test put-function
        run: cd put-function && go test -v ./ && cd ../../
  build-and-deploy-infra:
    needs: build-infra
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
      - uses: aws-actions/setup-sam@v1
      - uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1
      - run: sam build
        working-directory: ./
      - run: sam deploy --no-confirm-changeset --no-fail-on-empty-changeset
        working-directory: ./
  deploy-site:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: jakejarvis/s3-sync-action@master
        with:
          args: --delete
        env:
          AWS_S3_BUCKET: ronit-demo-site
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          SOURCE_DIR: ./resume-site
 ```
 
 - Push this repository to GitHub and at first it will throw error. Because the Secrets are not stored in the github repository. Add the secrets to the repository as shown below:
 
<img width="1312" alt="Screenshot 2022-07-07 at 2 06 30 PM" src="https://user-images.githubusercontent.com/91361382/177730012-81166847-f9b6-4719-a8e5-48259fa4fd40.png">

**Re-run the jobs from GitHub Actions**

This time it will be successfully executed !

So, Finally the Cloud Resume Challenge comes to an end from ```Day-2``` --> ```Day-10```

Our end Product of the Project is [https://ronitbanerjee.xyz](https://ronitbanerjee.xyz)

## Social Proof

<img width="1439" alt="Screenshot 2022-07-07 at 1 14 23 PM" src="https://user-images.githubusercontent.com/91361382/177731222-0498a273-283a-4507-aea8-6640ade5a99a.png">
