![placeholder image](https://s33046.pcdn.co/wp-content/uploads/2020/08/aws-sam-workflow-1.png)

# Deploy S3 using AWS SAM

## Introduction

Deployed an S3 Bucket and CloudFormation Stacks using the aws-sam-cli

## Use Case

- To store and retrieve any amount of data at any time from anywhere
- Object storage service that offers industry-leading scalability, data availability, security, and performance

## Cloud Research
 - Install aws-sam-cli (using Homebrew in Mac)
 ```
brew tap aws/tap
brew install aws-sam-cli
 ```
 - Set IAM user permissions (existing policies)
  • With Full access and administration access
	○ IAM
	○ IAM User
  ○ IAM UserChangePassword
 	○ API Gateway
 	○ Lambda
	○ CloudFormation

- Initialise the SAM in the directory of your choice (Your project folder in most case)
```
sam init
```
- My Arguments are as follows (Choose arguments according to your needs):

```
Which template source would you like to use?
	1 - AWS Quick Start Templates
	2 - Custom Template Location
Choice: 1

Choose an AWS Quick Start application template
	1 - Hello World Example
	2 - Multi-step workflow
	3 - Serverless API
	4 - Scheduled task
	5 - Standalone function
	6 - Data processing
	7 - Infrastructure event management
	8 - Machine Learning
Template: 1

Use the most popular runtime and package type? (Python and zip) [y/N]: n

Which runtime would you like to use?
	1 - dotnet6
	2 - dotnet5.0
	3 - dotnetcore3.1
	4 - go1.x
	5 - graalvm.java11 (provided.al2)
	6 - graalvm.java17 (provided.al2)
	7 - java11
	8 - java8.al2
	9 - java8
	10 - nodejs16.x
	11 - nodejs14.x
	12 - nodejs12.x
	13 - python3.9
	14 - python3.8
	15 - python3.7
	16 - python3.6
	17 - ruby2.7
	18 - rust (provided.al2)
Runtime: 4

What package type would you like to use?
	1 - Zip
	2 - Image
Package type: 1  

Based on your selections, the only dependency manager available is mod.
We will proceed copying the template using mod.

Would you like to enable X-Ray tracing on the function(s) in your application?  [y/N]: n

Project name [sam-app]: demo-sam-app  

Cloning from https://github.com/aws/aws-sam-cli-app-templates (process may take a moment)

    -----------------------
    Generating application:
    -----------------------
    Name: demo-sam-app
    Runtime: go1.x
    Architectures: x86_64
    Dependency Manager: mod
    Application Template: hello-world
    Output Directory: .
    
    Next steps can be found in the README file at ./demo-sam-app/README.md
        
```

- Enter the newly made folder by :
```
cd demo-sam-app
```

- Make a build :
```
sam build
```

- Go to AWS website and click on S3
- Create Bucket with a random name.
For reference :

![image](https://user-images.githubusercontent.com/91361382/176270165-7c3e327a-c584-46f2-bb50-b2a89fc68b93.png)


- Copy the name of the Bucket
- Change the default bucket name with the copied name in "samconfig.toml" file.
For reference, In line no. 6 :
<img width="513" alt="Screenshot 2022-06-29 at 12 48 18 AM" src="https://user-images.githubusercontent.com/91361382/176268135-f0c7a180-88cd-47ff-abba-ac080a0534c6.png">

- Final Deployment :

```
aws-vault exec [user-id] --no-session -- sam deploy --guided
```
Note: --guided is not required after one iteration of deployment, configurations are stored while first deployment is done.

- Deployment Arguments :

```
Configuring SAM deploy
======================

	Looking for config file [samconfig.toml] :  Not found

	Setting default arguments for 'sam deploy'
	=========================================
	Stack Name [sam-app]: demo-stack
	AWS Region [ap-south-1]: 
	#Shows you resources changes to be deployed and require a 'Y' to initiate deploy
	Confirm changes before deploy [y/N]: n
	#SAM needs permission to be able to create roles to connect to the resources in your template
	Allow SAM CLI IAM role creation [Y/n]: y
	#Preserves the state of previously provisioned resources when an operation fails
	Disable rollback [y/N]: n
	HelloWorldFunction may not have authorization defined, Is this okay? [y/N]: y
	Save arguments to configuration file [Y/n]: y
	SAM configuration file [samconfig.toml]: 
	SAM configuration environment [default]: 

```
- After few minutes, "Successfully created/updated stack - demo-stack in us-east-1" is displayed in the Terminal.

## Social Proof

![image](https://user-images.githubusercontent.com/91361382/176269798-262101a1-934f-4620-a3ec-1b728478723e.png)



