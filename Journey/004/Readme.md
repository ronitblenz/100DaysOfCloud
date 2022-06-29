![placeholder image](https://miro.medium.com/max/1400/1*EblFYpMbP0FR5DjDixD1Yw.png)

# Introduction to Infrastructure as a Code (IaaC) & Deploying HTML-CSS with AWS SDK

## Introduction

Learnt about IaaC and here are the important points that should be mentioned

 - What is IaaC?
 It is basically having your cloud configuration or infrastructure to find a source control like GitHub.
 
 - Benefits :
    1. Team Collaboration
    2. Disaster Recovery (Chaos Engineering)
    3. History of Changes (Version Controlling)
 
 - Tools :
    1. CloudFormation (AWS specific)
    2. AWS SAM (AWS Specific)
    3. Terraform (Works with every Cloud service)
    4. Pulumi (Not very popular, but similar to Terraform)
 
Apart from that, I deployed my sample resume site using AWS SDK
 
## Use Case

- Deployment
- Public Visibility

## Cloud Research

Here are the steps to deploy the HTML website in AWS :

 - To know the previous steps on How to Deploy S3 using AWS SAM, Click on [Day-2](https://github.com/ronitblenz/100DaysOfCloud/tree/main/Journey/003)
 
 - Add the following Snippet to the ```template.yaml``` below the resource tag
 (This creates a bucket named "ronit-demo-site", whose static website hosting is set to "Enabled")
 
 ```
   MyWebsite:
    Type: AWS::S3::Bucket
    Properties:
      AccessControl: PublicRead
      WebsiteConfiguration:
        IndexDocument: index.html
      BucketName: ronit-demo-site
 ```
 
 - Now make a folder for the HTML-CSS file and create the "index.html" inside that folder
 
 - Then, for a bit of automation, I updated the ```MakeFile``` to avoid repetition of CLI commands (Simply makes our lives easier, So why not?... Hehe)

Here is the snippet for the "MakeFile"

```
.PHONY: build

build:
	sam build

deploy-infra:
	sam build && aws-vault exec ronitblenz --no-session -- sam deploy

deploy-site:
	aws-vault exec ronitblenz --no-session -- aws s3 sync ./resume-site s3://ronit-demo-site
```

 - Now run command ```make deploy-site```

It uploads the .html file in the S3 Bucket

**But here is the catch, A case-study while clicking on the public S3 link :**

 1. Before uploading the .html file, it displayed ```Error 404 Not Found```
  It means, file does not exist!
  
  
    ![image](https://user-images.githubusercontent.com/91361382/176514141-10408c3b-b176-4acd-908e-424caacb2db3.png)

  
 2. After uploading the .html file, it displayed ```Error 403 Forbidden```
  It means, file exists but not accessible, permission not granted
  
  
    ![image](https://user-images.githubusercontent.com/91361382/176514191-fca6424e-57c5-48a1-a634-e493807ecf20.png)

 - Now I had to add Bucket Policies to the ```template.yaml``` file below MyWebsite tag (This helps to make all files in S3 Bucket accessible to the link)
Here is the snippet to be added :

```
BucketPolicy:
    Type: AWS::S3::BucketPolicyProperties:
      PolicyDocument:
        Id: MyPolicyVersion: 2012-10-17Statement:
          - Sid: PublicReadForGetBucketObjectsEffect: AllowPrincipal: "*"Action: "s3:GetObject"Resource: !Join- ""- - "arn:aws:s3:::"- !RefMyWebsite- /*Bucket: !Ref MyWebsite
```

 - Now run command ```make deploy-infra```

AND HOLA! You have successfully deployed your site on AWS.

## Social Proof


![image](https://user-images.githubusercontent.com/91361382/176507237-a2549610-adfe-4f2e-999d-93f09032600d.png)



