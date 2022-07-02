![placeholder image](https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2018/06/27/thumbnail.png)

# Deploying and Configuring Cloudfront from S3 Bucket

## Introduction

Customizing the Public link

 
## Use Case

- SSL Certificate Implementation
- Custom Domain
- Shortens the time and the link itself


## Cloud Research

Here are the steps for Deploying and Configuring Cloudfront from S3 Bucket :

 - Check the previous day documentations for the steps done till now regarding IAM, S3, CloudFormation
 
 - Add the following Snippet to the ```template.yaml``` below the resource tag
 (This creates a CDN in CloudFront)
 
 ```
MyDistribution:
    Type: "AWS::CloudFront::Distribution"
    Properties:
      DistributionConfig:
        DefaultCacheBehavior:
          ViewerProtocolPolicy: allow-all
          TargetOriginId: ronit-demo-site.s3-us-east-1.amazonaws.com
          DefaultTTL: 0
          MinTTL: 0
          MaxTTL: 0
          ForwardedValues:
            QueryString: false
        Origins:
          - DomainName: ronit-demo-site.s3-us-east-1.amazonaws.com
            Id: ronit-demo-site.s3-us-east-1.amazonaws.com
            CustomOriginConfig:
              OriginProtocolPolicy: match-viewer
        Enabled: "true"
        DefaultRootObject: index.html

 ```
 - Go to your IAM User Permissions in AWS Dashboard and give the permission ```CloudFrontFullAccess```
 (Else, it will not create a Distribution through CLI and throw an error)

 - Now run command ```make deploy-infra```

AND HOLA! You have successfully made a CloudFront Link for your site.

## Social Proof

<img width="1440" alt="Screenshot 2022-07-03 at 1 11 32 AM" src="https://user-images.githubusercontent.com/91361382/177014288-0d903aff-f363-4cca-a1ef-6b02f6ec92eb.png">

