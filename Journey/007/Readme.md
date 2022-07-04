![placeholder image](https://miro.medium.com/max/1039/1*enySPc_XesSQCUWc8i579Q.png)

# Disable CORS using API Gateway and AWS Lambda for Calling API using JavaScript

## Introduction

CORS is [Cross-Origin Resource Sharing](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

We will actually disable the CORS here
(Otherwise, it will throw CORS Error)
Then, Setup the Back-End of the Web application

## Use Case

- API Calls
- Add Dynamic Element to the Front-End


## Cloud Research

Here are the steps for Disabling CORS using API Gateway and AWS Lambda for Calling API using JavaScript :

 - Check the previous day documentations for the steps done till now regarding IAM, S3, CloudFormation, CloudFront and Certificate Manager
 
 - Open the ```main.go``` file
 
 - Add the following Snippet to the ```APIGateWayProxyResponse``` :
 (This adds additional Header property which will return the Headers from my API Request and disable the CORS)
Note: A small change to the body is also made here!

 ```
Headers: map[string]string{
    "Access-Control-Allow-Origin":  "*",
    "Access-Control-Allow-Methods": "*",
    "Access-Control-Allow-Headers": "*",
},
Body:       fmt.Sprintf("{ \"count\": \"2\" }"),
StatusCode: 200,
 ```
 
 - Run command ```make deploy-infra``` and check the following page address in AWS
 
 ![image](https://user-images.githubusercontent.com/91361382/177196947-237a6f4c-4b5e-41ee-ab7a-a08d41707d30.png)

 - There is an ```Invoke URL```. Copy and Paste it in a browser window to check if it is returning correct values

![image](https://user-images.githubusercontent.com/91361382/177197091-f559c326-411f-49fc-beee-f0827eaad6e3.png)

You can also check it through Terminal using "curl command"

![image](https://user-images.githubusercontent.com/91361382/177197153-995d20e9-9346-4603-9e2e-273ecf2d0c8f.png)


 - Now add the JavaScript Code in the ```index.html``` file
(This script fetches the Counter data through API)

```
<script>
    fetch('https://lyurpfjw7f.execute-api.us-east-1.amazonaws.com/Prod/hello/')
        .then(response => response.json())
        .then((data) => {
            document.getElementById('replaceme').innerText = data.count
        })
</script>
```
 - Also add this to the HTML for printing the values on page
 
 ```
<div class="d-flex flex-row-reverse">
    <div class="p2">View Count : <span id="replaceme"> </span></div>
    <div id="counter" class="bg-primary text-white p2"></div>
  </div>
 ```
 - Run command ```make deploy-site``` and check the deployed site
 (In my case, it is ```https://ronitbanerjee.xyz```)

AND The Back-End is ready to fetch data from the Database through API !

## Social Proof

![image](https://user-images.githubusercontent.com/91361382/177197701-ca3bfb79-f076-4af0-85cf-71f052beb60d.png)

