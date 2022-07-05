![placeholder image](https://miro.medium.com/max/1039/1*enySPc_XesSQCUWc8i579Q.png)

# Setup DynamoDB using AWS SAM

## Introduction

What is [DynamoDB](https://aws.amazon.com/dynamodb/)?
- It is a NoSQL proprietary Database by AWS
- It can sustain large amount of traffic and highly scalable
(It's not relevant in our case though)
- It is also Schema-less, So we don't need to define our data-types upfront

Here, we will setup the DynamoDB and change the configuration in the infrastructure


## Use Case

- Database
- API calls


## Cloud Research

Here are the steps for Setting up DynamoDB using AWS SAM :

 - Check the previous day documentations for the steps done till now regarding IAM, S3, CloudFormation, CloudFront, Certificate Manager and API GateWay
 
 - Add ```AmazonDynamoDBFullAccess``` Permission to the IAM user for executing the later tasks
 
 - Add the following Snippet to the ```template.yaml``` below Resource tab:
 (This adds a Table named "ronit-cloud-resume" in DynamoDB)

 ```
DynamoDBTable:
    Type: AWS::DynamoDB::Table
    Properties:
      TableName: ronit-cloud-resume
      BillingMode: PAY_PER_REQUEST
      AttributeDefinitions:
        - AttributeName: "ID"
          AttributeType: "S"
      KeySchema:
        - AttributeName: "ID"
          KeyType: "HASH"
 ```
 
 - Run command ```make deploy-infra``` and check the tables page in AWS DynamoDB Dashboard, and Click on the table we created via ```template.yaml```
 - Click on "Explore Items" and Create an item named ```example```
 
 ![image](https://user-images.githubusercontent.com/91361382/177382512-1c371314-cf8a-4969-a475-d47536e68b30.png)

**So, a Sample Table and Item is made in DynamoDB**

There are two types of Architectural Patterns --><br><br>
    1. **Monolithic Function** <br>(Putting all code in single Lambda Deployment)<br><br>
    2. **Single Purposed Function** <br>(Each Lambda per Functionality)<br>

We are using Single Purposed Function for our case

 - We will update the Lambda Functions in the ```template.yaml``` with the following snippet:
(It creates ```get``` and ```put``` funtions, deleting the existing ```HelloWorldFunction```

``` 
  GetFunction:
    Type: AWS::Serverless::Function 
    Properties:
      CodeUri: get-function/
      Handler: get-function
      Runtime: go1.x
      Architectures:
        - x86_64
      Events:
        CatchAll:
          Type: Api 
          Properties:
            Path: /get
            Method: GET
  PutFunction:
    Type: AWS::Serverless::Function 
    Properties:
      CodeUri: put-function/
      Handler: put-function
      Runtime: go1.x
      Architectures:
        - x86_64
      Events:
        CatchAll:
          Type: Api 
          Properties:
            Path: /put
            Method: GET
```


 - We also need to replace the ```Hello-world``` folder with ```get-function``` and ```put-function``` folders
 
 - Inside those folders, modify the ```go.mod``` for changing the function name into respective folder names

 - And lastly, Change the ```invoke URL``` in JavaScript snippet of ```index.html``` by replacing ```hello/``` with ```get```, as mentioned below :

```
<script>
    fetch('https://lyurpfjw7f.execute-api.us-east-1.amazonaws.com/Prod/get')
        .then(response => response.json())
        .then((data) => {
            document.getElementById('replaceme').innerText = data.count
        })
</script>
```

 - Run command ```make deploy-site``` and ```make deploy-infra``` to make changes to the stack
 - Check if the invoke link is returning { "count": "2" } in the Browser Window
 
![image](https://user-images.githubusercontent.com/91361382/177387118-e4d3670b-6318-490c-8e0a-f1240ae41bf5.png)

AND The DynamoDB is ready to store data over it and turn it Dynamic !

## Social Proof

![image](https://user-images.githubusercontent.com/91361382/177387684-779fd66f-5c1e-4558-865b-f7c0bf59899d.png)

**Representation of the Stages in the Table of DynamoDB after Deployment**

