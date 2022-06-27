![placeholder image](https://d1.awsstatic.com/howitworks_IAM_110321.8b2290727bb2022d54416e099c87ad9dc64be5d5.jpg)

# Setup IAM User in AWS

## Introduction

I made a IAM user through my Root account in AWS.
In addition, I stored the credentials in aws-vault which helps to execute commands faster and user-specific.

## Use Case

- Provides Separate space to work in
- Privacy
- Multi-user support
- SSH access from desktop terminal
- Root-user control

## Cloud Research

- Searched for "IAM" in AWS dashboard
- Setup MFA (Multi Factor Authentication) for root user [Mandatory]
 - Downloaded Google Authenticator app from playstore in my Android Device
 - Signed in with the details provided by AWS MFA portal
 - Clicked on Reveal Pin to get Token (refreshes every 30 second)
 
 - Create User
 - Added permissions (existing policies)
  • With Full access and administration access
	○ IAM
	○ IAM User
  ○ IAM UserChangePassword
 	○ API Gateway
 	○ Lambda
	○ CloudFormation

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

## Social Proof

![Screenshot 2022-06-27 at 11 10 44 PM](https://user-images.githubusercontent.com/91361382/176003201-dddf0e40-b240-45ff-b97d-53e5a49b0c08.png)

