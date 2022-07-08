![placeholder image](https://www.pedroalonso.net/static/2a6861df2748123c1a77570b3ecf385b/f6810/tf-aws.jpg)

# Managing Ubuntu EC2 Developer Environment using Terraform

## Introduction

I made an IAM user through my Root account in AWS.
In addition, I stored the credentials in aws-vault which helps to execute commands faster and user-specific.
Then, I installed Docker and Terraform in my local system
Finally, deployed an EC2 using Terraform

## Use Case

- Provides Developer Friendly Environment
- SSH access from desktop terminal
- Infrastructure Provisioning

## Cloud Research

**[STEP - 1 --> IAM and AWS-Vault Setup]**

- Searched for "IAM" in AWS dashboard
- Setup MFA (Multi Factor Authentication) for root user [Mandatory]
 - Downloaded Google Authenticator app from playstore in my Android Device
 - Signed in with the details provided by AWS MFA portal
 - Clicked on Reveal Pin to get Token (refreshes every 30 second)
 
 - Create User
 - Added permissions (existing policies)
  • AmazonEC2FullAccess

- Displays the Credentials (Download the .csv file or copy and store the credentials in a safe location, This is will not be displayed again)
- Incase you forgot to store the credentials, you need to create Access Key again and delete the previous one (Maximum limit of Access Key is 2)


<img width="1044" alt="image" src="https://user-images.githubusercontent.com/91361382/176001111-1dc61234-a4c4-4ee7-9259-8b5e607efc51.png">


- Setting Credentials using AWS-Vault :

```
aws-vault add [user-id]
```

- Asks for access_key_id and secret_access_key
- Copy and paste the credentials of the IAM user created


- Checks if the Credentials are stored correctly (Display Details of the Profile)

```
aws sts get-caller-identity
```

- You can also list the users and store more credentials with different user-id

```
aws-vault list             --> (Lists user)
aws-vault add [user-id]    --> (Adds more user)
```

**[STEP - 2 --> SSH Key and AWS Config]**

 - Check if SSH Key already exists in your local machine using the following Command :
 ```
 cat ~/.ssh/id_rsa.pub
 ```
 - Copy the Key Content
 
 If its not found, go to the same location and Generate SSH Key using the following Command :
 ```
 ssh-keygen -t rsa
 ```
 - Open EC2 in AWS Dashboard and Click on ```Key Pairs```
 - Go to ```Actions``` and then Import Key Pair
 - Name the key with anything you want (Please remember this Key Name, it will be needed later while using Terraform)
 - Paste the Key Content as done below :
 
![image](https://user-images.githubusercontent.com/91361382/178042765-10df5b17-40ec-4dac-bda3-9d3a4dad11f4.png)

 - Now, setup the AWS Config file using the following Command :
 ```
 vi ~/.aws/config 
 ```
 - Enter the region and mfa_serial (Check the IAM user details in AWS Dashboard) under the user created by aws-vault like this :
 ```
 [profile ronitblenz]
region=ap-south-1
mfa_serial=arn:aws:iam::22224xxxxxxx:mfa/[IAM-USER_NAME]
 ```
 
**[STEP - 3 --> Creating Docker Compose and Terraform Files]**

 - Create a ```docker-compose.yaml``` file and paste the following snippet :
 ```
version: '3.7'
services:
  tf:
    image: hashicorp/terraform:0.12.24
    volumes:
      - .:/infra
    working_dir: /infra
    environment:
      - AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
      - AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
 ```
 
 - Create a ```main.tf``` file and paste the following snippet :
 
 ```
provider "aws" {
  region  = "us-east-1"
  version = "~> 2.61.0"
}
resource "aws_instance" "web" {
  ami           = "ami-052efd3df9dad4825"
  instance_type = "t2.micro"
  key_name      = "finalkey"
  security_groups = [aws_security_group.web.name]
  tags = {
    Name = "WebServerByTf"
  }
}
resource "aws_security_group" "web" {
  name        = "web-security-group"
  description = "Allow access to our web server"
  ingress {
    description = "Allow SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
output "instance_public_dns" {
  value = aws_instance.web.public_dns
}
 ```
 - Turn on the Docker Daemon in Background (Else, the following commands will not be executed)
 
 - Initiate the Terraform Build
 ```
 docker-compose run --rm tf init
 ```
 
  - Shows the Tasks which are about to happen if the Terraform build is executed
 ```
 docker-compose run --rm tf plan
 ```
 
  - Execute the Terraform Build
 ```
 docker-compose run --rm tf apply
 ```
 - Type "yes" id asks for confirmation
 
 And, you have successfully created an EC2 Ubuntu instance over AWS using Terraform
 This can be used as a Testing Environment by Developers or Cloud Engineers.
 
 
<img width="717" alt="image" src="https://user-images.githubusercontent.com/91361382/178044087-47f864af-2f29-41f8-867c-c7e655c79abe.png">


## Social Proof

<img width="1057" alt="image" src="https://user-images.githubusercontent.com/91361382/178044112-bfef91ea-fec2-4ad9-97ef-ce26988e65c4.png">

**Up and running Ubuntu Environment over AWS EC2 using Terraform**


