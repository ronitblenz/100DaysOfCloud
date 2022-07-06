![placeholder image](https://miro.medium.com/max/1039/1*enySPc_XesSQCUWc8i579Q.png)

# Store and Get Data from DynamoDB

## Introduction


What is [DynamoDB](https://aws.amazon.com/dynamodb/)?
- It is a NoSQL proprietary Database by AWS
- It can sustain large amount of traffic and highly scalable
(It's not relevant in our case though)
- It is also Schema-less, So we don't need to define our data-types upfront

Here, we will connect the database to the backend of the site while configuring the Lambda functions. 
This will enable the website to show the Visitor Count.


## Use Case

- Database
- API calls


## Cloud Research

Here are the steps for Storing and Getting Data from DynamoDB :

 - Check the previous day documentations for the steps done till now regarding IAM, S3, CloudFormation, CloudFront, Certificate Manager and API GateWay
 
**1. PUT FUNCTION**
 - Firstly, Modify the ```go.mod```, ```go.sum``` and ```main.go``` files

**go.mod -->**

```
require github.com/aws/aws-lambda-go v1.23.0
require github.com/aws/aws-sdk-go v1.38.17
require github.com/cpuguy83/go-md2man/v2 v2.0.0
replace gopkg.in/yaml.v2 => gopkg.in/yaml.v2 v2.2.8
module put-function
go 1.16
```

**go.sum -->**

```
github.com/BurntSushi/toml v0.3.1/go.mod h1:xHWCNGjB5oqiDr8zfno3MHue2Ht5sIBksp03qcyfWMU=
github.com/appleboy/go-fcm v0.1.5 h1:fKbcZf/7vwGsvDkcop8a+kCHnK+tt4wXX0X7uEzwI6E=
github.com/appleboy/go-fcm v0.1.5/go.mod h1:MSxZ4LqGRsnywOjnlXJXMqbjZrG4vf+0oHitfC9HRH0=
github.com/aws/aws-lambda-go v1.23.0 h1:Vjwow5COkFJp7GePkk9kjAo/DyX36b7wVPKwseQZbRo=
github.com/aws/aws-lambda-go v1.23.0/go.mod h1:jJmlefzPfGnckuHdXX7/80O3BvUUi12XOkbv4w9SGLU=
github.com/aws/aws-sdk-go v1.38.17 h1:1OfcfEtNrphUZYa+J0U35/1hxePbb3ASSQWdFS7L0Hs=
github.com/aws/aws-sdk-go v1.38.17/go.mod h1:hcU610XS61/+aQV88ixoOzUoG7v3b31pl2zKMmprdro=
github.com/cpuguy83/go-md2man/v2 v2.0.0-20190314233015-f79a8a8ca69d/go.mod h1:maD7wRr/U5Z6m/iR4s+kqSMx2CaBsrgA7czyZG/E6dU=
github.com/cpuguy83/go-md2man/v2 v2.0.0/go.mod h1:maD7wRr/U5Z6m/iR4s+kqSMx2CaBsrgA7czyZG/E6dU=
github.com/davecgh/go-spew v1.1.0/go.mod h1:J7Y8YcW2NihsgmVo/mv3lAwl/skON4iLHjSsI+c5H38=
github.com/davecgh/go-spew v1.1.1 h1:vj9j/u1bqnvCEfJOwUhtlOARqs3+rkHYY13jYWTU97c=
github.com/davecgh/go-spew v1.1.1/go.mod h1:J7Y8YcW2NihsgmVo/mv3lAwl/skON4iLHjSsI+c5H38=
github.com/dgrijalva/jwt-go v3.2.0+incompatible h1:7qlOGliEKZXTDg6OTjfoBKDXWrumCAMpl/TFQ4/5kLM=
github.com/dgrijalva/jwt-go v3.2.0+incompatible/go.mod h1:E3ru+11k8xSBh+hMPgOLZmtrrCbhqsmaPHjLKYnJCaQ=
github.com/go-test/deep v1.0.4 h1:u2CU3YKy9I2pmu9pX0eq50wCgjfGIt539SqR7FbHiho=
github.com/go-test/deep v1.0.4/go.mod h1:wGDj63lr65AM2AQyKZd/NYHGb0R+1RLqB8NKt3aSFNA=
github.com/gorilla/websocket v1.4.2 h1:+/TMaTYc4QFitKJxsQ7Yye35DkWvkdLcvGKqM+x0Ufc=
github.com/gorilla/websocket v1.4.2/go.mod h1:YR8l580nyteQvAITg2hZ9XVh4b55+EU/adAjf1fMHhE=
github.com/hashicorp/go-version v1.3.0 h1:McDWVJIU/y+u1BRV06dPaLfLCaT7fUTJLp5r04x7iNw=
github.com/hashicorp/go-version v1.3.0/go.mod h1:fltr4n8CU8Ke44wwGCBoEymUuxUHl09ZGVZPK5anwXA=
github.com/jmespath/go-jmespath v0.4.0 h1:BEgLn5cpjn8UN1mAw4NjwDrS35OdebyEtFe+9YPoQUg=
github.com/jmespath/go-jmespath v0.4.0/go.mod h1:T8mJZnbsbmF+m6zOOFylbeCJqk5+pHWvzYPziyZiYoo=
github.com/jmespath/go-jmespath/internal/testify v1.5.1 h1:shLQSRRSCCPj3f2gpwzGwWFoC7ycTf1rcQZHOlsJ6N8=
github.com/jmespath/go-jmespath/internal/testify v1.5.1/go.mod h1:L3OGu8Wl2/fWfCI6z80xFu9LTZmf1ZRjMHUOPmWr69U=
github.com/moemoe89/go-localization v1.0.0 h1:EcBH2ap/nS28jbnJ5sayGXfSKbV8KIpIfgpYPhQAnsc=
github.com/moemoe89/go-localization v1.0.0/go.mod h1:kZuSPnxZ2HcVC9SsShfVpHs+Kbx/KgeUP15jx8VgKG8=
github.com/pkg/errors v0.8.0/go.mod h1:bwawxfHBFNV+L2hUp1rHADufV3IMtnDRdf1r5NINEl0=
github.com/pkg/errors v0.9.1 h1:FEBLx1zS214owpjy7qsBeixbURkuhQAwrK5UwLGTwt4=
github.com/pkg/errors v0.9.1/go.mod h1:bwawxfHBFNV+L2hUp1rHADufV3IMtnDRdf1r5NINEl0=
github.com/pmezard/go-difflib v1.0.0 h1:4DBwDE0NGyQoBHbLQYPwSUPoCMWR5BEzIk/f1lZbAQM=
github.com/pmezard/go-difflib v1.0.0/go.mod h1:iKH77koFhYxTK1pcRnkKkqfTogsbg7gZNVY4sRDYZ/4=
github.com/russross/blackfriday/v2 v2.0.1/go.mod h1:+Rmxgy9KzJVeS9/2gXHxylqXiyQDYRxCVz55jmeOWTM=
github.com/satori/go.uuid v1.2.0 h1:0uYX9dsZ2yD7q2RtLRtPSdGDWzjeM3TbMJP9utgA0ww=
github.com/satori/go.uuid v1.2.0/go.mod h1:dA0hQrYB0VpLJoorglMZABFdXlWrHn1NEOzdhQKdks0=
github.com/shurcooL/sanitized_anchor_name v1.0.0/go.mod h1:1NzhyTcUVG4SuEtjjoZeVRXNmyL/1OwPU0+IJeTBvfc=
github.com/slack-go/slack v0.8.2 h1:D7jNu0AInBfdQ4QyKPtVSp+ZxQes3EzWW17RZ/va4JE=
github.com/slack-go/slack v0.8.2/go.mod h1:FGqNzJBmxIsZURAxh2a8D21AnOVvvXZvGligs4npPUM=
github.com/stretchr/objx v0.1.0/go.mod h1:HFkY916IF+rwdDfMAkV7OtwuqBVzrE8GR6GFx+wExME=
github.com/stretchr/testify v1.2.2/go.mod h1:a8OnRcib4nhh0OaRAV+Yts87kKdq0PP7pXfy6kDkUVs=
github.com/stretchr/testify v1.6.1 h1:hDPOHmpOpP40lSULcqw7IrRb/u7w6RpDC9399XyoNd0=
github.com/stretchr/testify v1.6.1/go.mod h1:6Fq8oRcR53rry900zMqJjRRixrwX3KX962/h/Wwjteg=
github.com/urfave/cli/v2 v2.2.0/go.mod h1:SE9GqnLQmjVa0iPEY0f1w3ygNIYcIJ0OKPMoW2caLfQ=
golang.org/x/crypto v0.0.0-20190308221718-c2843e01d9a2/go.mod h1:djNgcEr1/C05ACkg1iLfiJU5Ep61QUkGW8qpdssI0+w=
golang.org/x/crypto v0.0.0-20200622213623-75b288015ac9/go.mod h1:LzIPMQfyMNhhGPhUkYOs5KpL4U8rLKemX1yGLhDgUto=
golang.org/x/net v0.0.0-20190404232315-eb5bcb51f2a3/go.mod h1:t9HGtf8HONx5eT2rtn7q6eTqICYqUVnKs3thJo3Qplg=
golang.org/x/net v0.0.0-20201110031124-69a78807bb2b h1:uwuIcX0g4Yl1NC5XAz37xsr2lTtcqevgzYNVt49waME=
golang.org/x/net v0.0.0-20201110031124-69a78807bb2b/go.mod h1:sp8m0HH+o8qH0wwXwYZr8TS3Oi6o0r6Gce1SSxlDquU=
golang.org/x/sys v0.0.0-20190215142949-d0b11bdaac8a/go.mod h1:STP8DvDyc/dI5b8T5hshtkjS+E42TnysNCUPdjciGhY=
golang.org/x/sys v0.0.0-20190412213103-97732733099d/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/sys v0.0.0-20200930185726-fdedc70b468f/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/text v0.3.0/go.mod h1:NqM8EUOU14njkJ3fqMW+pc6Ldnwhi/IjpwHt7yyuwOQ=
golang.org/x/text v0.3.3 h1:cokOdA+Jmi5PJGXLlLllQSgYigAEfHXJAERHVMaCc2k=
golang.org/x/text v0.3.3/go.mod h1:5Zoc/QRtKVWzQhOtBMvqHzDpF6irO9z98xDceosuGiQ=
golang.org/x/tools v0.0.0-20180917221912-90fa682c2a6e/go.mod h1:n7NCudcB/nEzxVGmLbDWY5pfWTLqBcC2KZ6jyYvM4mQ=
gopkg.in/check.v1 v0.0.0-20161208181325-20d25e280405 h1:yhCVgyC4o1eVCa2tZl7eS0r+SDo693bJlVdllGtEeKM=
gopkg.in/check.v1 v0.0.0-20161208181325-20d25e280405/go.mod h1:Co6ibVJAznAaIkqp8huTwlJQCZ016jof/cbN4VW5Yz0=
gopkg.in/yaml.v2 v2.2.2/go.mod h1:hI93XBmqTisBFMUTm0b8Fm+jr3Dg1NNxqwp+5A1VGuI=
gopkg.in/yaml.v2 v2.2.8 h1:obN1ZagJSUGI0Ek/LBmuj4SNLPfIny3KsKFopxRdj10=
gopkg.in/yaml.v2 v2.2.8/go.mod h1:hI93XBmqTisBFMUTm0b8Fm+jr3Dg1NNxqwp+5A1VGuI=
gopkg.in/yaml.v3 v3.0.0-20200313102051-9f266ea9e77c/go.mod h1:K4uyk7z7BCEPqu6E+C64Yfv1cQ7kz7rIZviUmN+EgEM=
gopkg.in/yaml.v3 v3.0.0-20200615113413-eeeca48fe776 h1:tQIYjPdBoyREyB9XMu+nnTclpTYkz2zFM+lzLJFO4gQ=
gopkg.in/yaml.v3 v3.0.0-20200615113413-eeeca48fe776/go.mod h1:K4uyk7z7BCEPqu6E+C64Yfv1cQ7kz7rIZviUmN+EgEM=
```

**main.go -->**

```
package main
import (
    "log"
    
    "github.com/aws/aws-lambda-go/events"
    "github.com/aws/aws-lambda-go/lambda"
    "github.com/aws/aws-sdk-go/aws"
    "github.com/aws/aws-sdk-go/aws/session"
    "github.com/aws/aws-sdk-go/service/dynamodb"
)
func handler(request events.APIGatewayProxyRequest) (events.APIGatewayProxyResponse, error) {
    
    sess := session.Must(session.NewSessionWithOptions(session.Options{
        SharedConfigState: session.SharedConfigEnable,
    }))
    svc := dynamodb.New(sess)
    input := &dynamodb.UpdateItemInput{
        TableName: aws.String("ronit-cloud-resume"),
        Key: map[string]*dynamodb.AttributeValue{
            "ID": {
                S: aws.String("visitors"),
            },
        },
        UpdateExpression: aws.String("ADD visitors :inc"),
        ExpressionAttributeValues: map[string]*dynamodb.AttributeValue{
            ":inc": {
                N: aws.String("1"),
            },
        },
    }
    _, err := svc.UpdateItem(input)
    if err != nil {
        log.Fatalf("Got error calling UpdateItem: %s", err)
    }
    return events.APIGatewayProxyResponse{
        Headers: map[string]string{
            "Access-Control-Allow-Origin":  "*",
            "Access-Control-Allow-Methods": "*",
            "Access-Control-Allow-Headers": "*",
        },
        StatusCode: 200,
    }, nil
}
func main() {
    lambda.Start(handler)
}
```
 - Update the ```PutFunction``` in ```template.yaml``` :

```
  PutFunction:
    Type: AWS::Serverless::Function 
    Properties:
      Policies:
        - DynamoDBCrudPolicy:
            TableName: ronit-cloud-resume
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

 - Run command ```make deploy-infra``` and check the tables page in AWS DynamoDB Dashboard, and Click on the table
 - Click on "Scan/Query Items" and write ```visitors``` in ID (Partition Key)
 - Click on Run and check the visitor count like this :

 ![Jul-06-2022 18-18-20](https://user-images.githubusercontent.com/91361382/177622519-9b5942ab-74d8-47c5-a9fc-ba9277e80377.gif)


**2. GET FUNCTION**
 - As previously done, Modify the ```go.mod```, ```go.sum``` and ```main.go``` files
**Note: go.mod and go.sum will be same for this case, just copy and paste the code from above**

**main.go -->**

``` 
package main
import (
    "log"
    "fmt"
    "github.com/aws/aws-lambda-go/events"
    "github.com/aws/aws-lambda-go/lambda"
    "github.com/aws/aws-sdk-go/aws"
    "github.com/aws/aws-sdk-go/aws/session"
    "github.com/aws/aws-sdk-go/service/dynamodb"
    "github.com/aws/aws-sdk-go/service/dynamodb/dynamodbattribute"
)
func handler(request events.APIGatewayProxyRequest) (events.APIGatewayProxyResponse, error) {
    
    sess := session.Must(session.NewSessionWithOptions(session.Options{
        SharedConfigState: session.SharedConfigEnable,
    }))
    svc := dynamodb.New(sess)
    var input = &dynamodb.GetItemInput{
        TableName: aws.String("ronit-cloud-resume"),
        Key: map[string]*dynamodb.AttributeValue{
            "ID": {
                S: aws.String("visitors"),
            },
        },
    }
    queryOutput, err := svc.GetItem(input)
    type Count struct {
        ID       string `json:"ID"`
        Visitors string `json:"visitors"`
    }
    count := Count{}
    err = dynamodbattribute.UnmarshalMap(queryOutput.Item, &count)
    if err != nil {
        log.Fatalf("Got error calling UpdateItem: %s", err)
    }
    return events.APIGatewayProxyResponse{
        Headers: map[string]string{
            "Access-Control-Allow-Origin":  "*",
            "Access-Control-Allow-Methods": "*",
            "Access-Control-Allow-Headers": "*",
        },
        Body:       fmt.Sprintf("{ \"count\": \"%s\" }", count.Visitors),
        StatusCode: 200,
    }, nil
}
func main() {
    lambda.Start(handler)
}
```
 - Update the ```GetFunction``` in ```template.yaml``` :

``` 
  GetFunction:
    Type: AWS::Serverless::Function
    Properties:
      Policies:
       - DynamoDBCrudPolicy:
            TableName: ronit-cloud-resume
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
```

 - Now update the JavaScript in ```index.html``` to exchange values with dynamodb and update the counter in Front-end :

```
<script>
    fetch('https://lyurpfjw7f.execute-api.us-east-1.amazonaws.com/Prod/put')
        .then(() => fetch('https://lyurpfjw7f.execute-api.us-east-1.amazonaws.com/Prod/get'))
        .then(response => response.json())
        .then((data) => {
            document.getElementById('replaceme').innerText = data.count
        })
</script>
```

 - Run command ```make deploy-site``` and ```make deploy-infra``` to make changes to the stack and site

 - Check if your Viewer Count is updating on your Website while refreshing everytime

AND The database is connected to the site !

## Social Proof

![image](https://user-images.githubusercontent.com/91361382/177624409-734ee614-f27a-4d6d-8b54-6f99c1a5bbe8.png)


**Dynamic Counter added to the website which keeps track of the view counts on the website**

