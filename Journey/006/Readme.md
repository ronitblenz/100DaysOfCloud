![placeholder image](https://miro.medium.com/max/1838/1*778ypl8euW0poV8WpTp_lw.png)

# Configure AWS Route 53, CloudFront and SSL Certificate

## Introduction

We will learn how to deploy a serverless site from CloudFront using Route 53 and also add SSL Certficate using ACM (Amazon Certificate Manager)

## Use Case

- HTTPS (Secured Protocol with SSL Certificate)
- Custom Domain


## Cloud Research

Here are the steps for Configuring AWS Route 53, CloudFront and SSL Certificate :

 - Check the previous day documentations for the steps done till now regarding IAM, S3, CloudFormation and CloudFront
 
 - Add the following Snippet to the ```template.yaml``` below the resource tag
 (This creates a Record in Route 53)
 
 ```
MyRoute53Record:
    Type: "AWS::Route53::RecordSetGroup"
    Properties:
      HostedZoneId: Z04723851ZV06PPOSS6A2 # TODO: Don't hardcode me
      RecordSets:
        - Name: ronitbanerjee.xyz # TODO: Don't hardcode me
          Type: A
          AliasTarget:
            HostedZoneId: Z2FDTNDATAQYW2  # This is CloudFront HostedZoneId (Constant)
            DNSName: !GetAtt MyDistribution.DomainName
 ```
 For instance, My domain provider is ".xyz"
 - Login to your "Manage Domain" page in your Domain Provider's dashboard
 - Copy the Name Servers from Hosted Zones in Route53 and paste it in the Custom Name Servers of Domain Provider's dashboard as shown below
 
From Route53:
![image](https://user-images.githubusercontent.com/91361382/177051906-13497a87-66f4-4525-acbb-ffb4a1fba42a.png)

To Domain Management Page:
![image](https://user-images.githubusercontent.com/91361382/177051908-d379f36c-01d6-4504-92c6-cd99f379b4fc.png)

Please wait for few hours, it takes time for DNS Propagation

Now it will definitely throw an error, because the process is not completed yet. 
If you see this screen mentioned below, the above steps are followed correctly


![image](https://user-images.githubusercontent.com/91361382/177052038-754cd438-05bd-4d24-99a3-3360bd3776b7.png)

 - Now, ACM (Amazon Certificate Manager) will come into picture
 - Go to ACM in AWS Dashboard
 - Click on "Request" for a certificate and mention your domain name
 (For Example: ```ronitbanerjee.xyz``` in my case)
 - Now verify via DNS Method
    1. An option to create CNAME automatically will be present
    2. Click on that and wait for 5 minutes
    3. This will complete the verification process for the SSL Certificate
    
 - Go to your IAM User Permissions in AWS Dashboard and give the permission ```AWSCertificateManagerFullAccess```
 (Else, it will not make the required changes for HTTPS and throw an error)
 
 - Add the following Snippet to the ```template.yaml``` in the MyCertificate tag and Update MyDistribution tag
 (This adds the Certificate to your Custom Domain)
 
 ```
MyCertificate:
    Type: AWS::CertificateManager::Certificate
    Properties:
      DomainName: ronitbanerjee.xyz # TODO: Don't hardcode me
      ValidationMethod: DNS
      
     
  # MyDistribution:
    # Properties:
      # DistributionConfig:
        ViewerCertificate:
            AcmCertificateArn: !Ref MyCertificate
            SslSupportMethod: sni-only
 ```

 - Now run command ```make deploy-infra```
 - Lastly, add "Alternate Domain" as ```ronitbanerjee.xyz``` in the CloudFront CDN.

AND HOLA! Custom Domain Site is Deployed with HTTPS Protocol

## Social Proof


![image](https://user-images.githubusercontent.com/91361382/177052392-30456b3b-66be-4f2f-bf3b-740d5027313f.png)

