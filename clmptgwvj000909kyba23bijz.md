---
title: "Mastering AWS Lambda: Deploying a Node.js Serverless Function with the Serverless Framework"
seoTitle: "Master AWS Lambda: Deploy Node.js Serverless Functions with Serverless"
seoDescription: "Learn AWS Lambda basics and deploy serverless Node.js functions using the Serverless Framework. Start your serverless journey today"
datePublished: Tue Sep 19 2023 04:30:09 GMT+0000 (Coordinated Universal Time)
cuid: clmptgwvj000909kyba23bijz
slug: mastering-aws-lambda-deploying-a-nodejs-serverless-function-with-the-serverless-framework
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694860784641/21768aca-3e70-43a7-904f-ac4c79fc82a6.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1694861091958/e7248d92-68da-4503-af82-1e005e377fd6.png
tags: cloud, aws, nodejs, serverless, aws-lambda

---

![](https://cdn-images-1.medium.com/max/800/1*PJy_cjmNMIPwD9hNSsaaXA.png align="left")

### **Introduction**

Welcome to the world of AWS Lambda, a cornerstone of serverless computing. In this comprehensive guide, you’ll learn how to deploy a Node.js serverless function using AWS Lambda and the Serverless Framework. Whether you’re new to Lambda or want to deepen your practical knowledge, you’re in the right place.

### Chapter 1: Understanding Serverless Computing

#### What is Serverless Computing?

Serverless computing is a cloud computing model that allows you to build and run applications without the need to manage the underlying infrastructure. In a serverless architecture, cloud providers like AWS take care of server provisioning, scaling, and maintenance, allowing you to focus solely on your application code.

#### EC2 vs. Serverless

**Amazon EC2 (Elastic Compute Cloud)**

1. Requires manual provisioning and management of virtual machines (EC2 instances).
    
2. Scaling is manual or requires complex auto-scaling configurations.
    
3. You pay for reserved or on-demand instances, regardless of actual usage.
    
4. Ideal for traditional applications requiring full control over the server environment.
    

**Serverless (AWS Lambda)**

1. No need to manage servers; AWS Lambda handles infrastructure for you.
    
2. Auto-scales automatically based on incoming traffic.
    
3. Pay only for the compute time your functions consume.
    
4. Perfect for event-driven, highly scalable, and cost-effective applications.
    

#### Advantages of Serverless Computing

1. Cost-Efficiency: Pay only for what you use, with no upfront costs or idle resources.
    
2. Auto-Scaling: Automatically handle traffic spikes without manual intervention.
    
3. Managed Infrastructure: Focus on code, while cloud providers manage servers, networking, and security.
    
4. Event-Driven: Easily integrate with various AWS services and trigger functions based on events.
    
5. Global Reach: Deploy functions in multiple regions for low-latency access worldwide.
    

#### Disadvantages of Serverless Computing

1. Vendor Lock-In: Code written for one provider may not be easily portable to another.
    
2. Cold Starts: Initial invocation of a function can experience latency due to resource provisioning.
    
3. Limited Execution Time: Functions are typically limited in runtime, which may not be suitable for long-running tasks.
    

### Chapter 2: Prerequisites

Before we dive into deploying our serverless function, make sure you have the following prerequisites in place:

* An AWS account: If you don’t have one, you can sign up for a free AWS account [here](https://aws.amazon.com/free/).
    

![](https://cdn-images-1.medium.com/max/800/1*p-WAyzvYnCBQD840o7Y-Vg.png align="left")

* Node.js and npm installed: You can download Node.js and npm from the official website [here](https://nodejs.org/).
    

![](https://cdn-images-1.medium.com/max/800/1*0cHpAHUCBC0abwtXl47xzQ.png align="left")

* Serverless Framework installed: To install the Serverless Framework, run the following command in your terminal:
    

```javascript
npm install -g serverless
```

![](https://cdn-images-1.medium.com/max/800/1*4R4Z1HepoZgmhUqjM5vPAA.png align="left")

Configuring AWS Access Keys

1. If you haven’t already, you need to configure your AWS access keys. These keys consist of an Access Key ID and a Secret Access Key and are required for the Serverless Framework to interact with your AWS resources.
    
2. To configure your AWS access keys, open your terminal and run the following command:
    

```java
aws configure
```

 3. You’ll be prompted to enter your AWS Access Key ID, Secret Access Key, default region, and default output format. You can obtain these keys from your AWS IAM (Identity and Access Management) dashboard.

* Access your AWS IAM dashboard by logging in to your AWS account.
    

![](https://cdn-images-1.medium.com/max/800/1*OKfCHlgC8VnVsFU4WdOY5Q.png align="left")

* In the IAM dashboard, navigate to “Users” and select your user (or create a new one if necessary).
    

![](https://cdn-images-1.medium.com/max/800/1*gtNp2rUnQTafFN5XCT1ZXQ.png align="left")

* In the “Security credentials” tab, you can generate and retrieve your Access Key ID and Secret Access Key.
    

![](https://cdn-images-1.medium.com/max/800/1*EXuOeRe34s2BjCmz91-w9w.png align="left")

![](https://cdn-images-1.medium.com/max/800/1*cW5TU-GpN8Xnf9jMFPqEqQ.png align="left")

![](https://cdn-images-1.medium.com/max/800/1*wY1gCiMJhLoI7YQanL6Z0g.png align="left")

* Enter these values when prompted by the `aws configure` command.|
    

![](https://cdn-images-1.medium.com/max/800/1*IlFe62qrOz6lxSvtAc3z6w.png align="left")

### Chapter 3: Creating a Serverless Service

1. Open your terminal and create a new directory for your serverless project:
    

```java
mkdir serverless-nodejs-app
cd serverless-nodejs-app
```

1. Initialize a new Serverless service using the following command:
    

```java
serverless create -t aws-nodejs -n serverless-nodejs-app
```

This command generates the necessary boilerplate code for a Node. js-based serverless service.

![](https://cdn-images-1.medium.com/max/800/1*4gmljC7Zll5lEi-jdsmi8A.png align="left")

### Chapter 4: Configuring the Serverless Framework

1. Navigate to the newly created `serverless-nodejs-app` directory.
    
2. Open the `serverless.yml` file and adjust the configuration to your preferences. You can specify the AWS region, stage, and other settings.
    

```java
service: serverless-nodejs-app
provider:
  name: aws
  runtime: nodejs14.x
  stage: dev
  region: ap-south-1 # Change to your desired AWS region
functions:
  app:
    handler: handler.handler
    events:
      - http:
          path: /
          method: ANY
```

### Chapter 5: Creating a GET Request Handler

1. Inside your `serverless-nodejs-app` directory, you should have a file named `handler.js`. This is where you define your Lambda function handler.
    
2. Open the `handler.js` file in your code editor and modify it to include a simple GET request handler that returns "Hello from [blog.anilgulati.tech](http://blog.anilgulati.tech)." Here's an example of what the `handler.js` file could look like:
    

```java
// handler.js
module.exports.hello = async (event) => {
  return {
    statusCode: 200,
    body: JSON.stringify({ message: 'Hello from blog.anilgulati.tech' }),
  };
};
```

In this code, we defined an `async` function called `hello` that takes an `event` as its parameter. This function returns a response with a 200 status code and the message "Hello from [blog.anilgulati.tech](http://blog.anilgulati.tech)."

1. Save the changes to the `handler.js` file.
    

### Chapter 6: Defining the Function in serverless.yml

Now, let’s update the `serverless.yml` file to specify this function:

```java
service: serverless-nodejs-app
provider:
  name: aws
  runtime: nodejs14.x
  stage: dev
  region: ap-south-1 # Change to your desired AWS region
functions:
  app:
    handler: handler.hello # Update the handler to point to the hello function
    events:
      - http:
          path: /
          method: ANY
```

Make sure to update the `handler` field to point to the `handler.hello` function, as shown above.

### Chapter 7: Deploying Your Serverless Function

1. Deploy your serverless function by running the following command:
    

```java
serverless deploy
```

This command packages your application, creates the necessary AWS resources, and deploys your function.

1. After the deployment is complete, you’ll receive a URL where your serverless function is accessible. It will look something like this: [`https://your-api-id.execute-api.us-east-1.amazonaws.com/dev/`](https://your-api-id.execute-api.us-east-1.amazonaws.com/dev/)[.](https://your-api-id.execute-api.us-east-1.amazonaws.com/dev/.)
    

![](https://cdn-images-1.medium.com/max/800/1*hpJ4hKNyGsGqLqKodHtoQA.png align="left")

### Chapter 8: Testing Your Serverless Function

1. Open a web browser or use a tool like `curl` to send a GET request to your function's URL. You should receive the "Hello from your serverless function!" response.
    

![](https://cdn-images-1.medium.com/max/800/1*scFlS-_ul5tTsTavydJHwA.png align="left")

 2. You can also test your function locally using the Serverless Framework. Run the following command to invoke your function locally:

```java
serverless invoke local -f app
```

![](https://cdn-images-1.medium.com/max/800/1*mmdG2q0zAUYU09eaY3QOBA.png align="left")

### Chapter 9: Deploying to Production

To deploy your serverless function to a production environment, modify the `serverless.yml` file by changing the `stage` to `production`.

```java
provider:
  name: aws
  runtime: nodejs14.x
  stage: production
  region: us-east-1 # Change to your desired AWS region
```

Then, redeploy your function using `serverless deploy`.

![](https://cdn-images-1.medium.com/max/800/1*D93GOclhM-snw3vtxF10bg.png align="left")

Conclusion: Congratulations! You’ve successfully deployed a Node.js serverless function using AWS Lambda and the Serverless Framework. This is just the beginning of your serverless journey. Explore more advanced features of AWS Lambda, optimize your serverless functions for performance and cost-efficiency, and continue building amazing serverless applications.

External Links: For further exploration, refer to the official [AWS Lambda documentation](https://docs.aws.amazon.com/lambda/) and the [Serverless Framework documentation](https://www.serverless.com/framework/docs/).  
  
**Enjoyed This Article?**

> ***If you enjoy reading this post, got help, knowledge through it, and want to support my efforts please clap this article and follow.  
> To explore more of my work, visit my portfolio at*** [***anilgulati.tech***](http://anilgulati.tech?utmSource=hashnode&article=AWS-Lambda)