---
title: "Getting Started with Amazon EC2: Launching Your First Linux Instance"
seoTitle: "Getting Started with Amazon EC2: Launching Your First Linux Instance"
seoDescription: "Learn to Launch Amazon EC2 Instances: A Step-by-Step Guide to AWS Cloud Computing for Beginners with Linux Instances"
datePublished: Sun Sep 17 2023 04:30:10 GMT+0000 (Coordinated Universal Time)
cuid: clmmyl7vw000109l9higngrsq
slug: getting-started-with-amazon-ec2-launching-your-first-linux-instance
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694818501077/3f4424a2-247d-4aa3-9f8c-4b2da2b920b5.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1694818666400/5acccf2e-75f6-4aff-8282-a75f42144582.png
tags: ec2, linux, aws, wsl, aws-ec2

---

![](https://cdn-images-1.medium.com/max/800/1*MBNnFCpC7tCiCmjOFP2JXg.png align="center")

Amazon Elastic Compute Cloud (Amazon EC2) is a cornerstone service in Amazon Web Services (AWS) that allows you to launch and manage virtual machines, known as instances, in the cloud. In this guide, we’ll walk you through the process of launching your first EC2 instance using the AWS Management Console. We’ll be using a Linux-based instance type, specifically the t2.micro, which is often eligible for the AWS Free Tier (note: eligibility may vary by region and usage, so consult AWS documentation for the latest information). Let’s dive in!

### Step 1: Logging into the AWS Console

* Begin by logging into the [AWS Management Console](https://aws.amazon.com/).
    

![](https://cdn-images-1.medium.com/max/800/1*bsOBRoK67Fl6ais39TysoQ.png align="left")

### Step 2: Accessing the EC2 Dashboard

* Once logged in, navigate to the EC2 dashboard by clicking on “Services” at the top left corner, then selecting “EC2” under the “Compute” section.
    

![](https://cdn-images-1.medium.com/max/800/1*oZ-iWfwHWgZnGg6PpNuHZg.png align="left")

### Step 3: Launching an EC2 Instance

* Click on the “Launch Instance” button to initiate the instance creation process.
    

![](https://cdn-images-1.medium.com/max/800/1*d8OjlSB80CbSIgFV31TqBg.png align="left")

### Step 4: Choosing an OS Image

* In this example, we’ll select a Ubuntu AMI. The AMI serves as the template for your virtual machine.
    

![](https://cdn-images-1.medium.com/max/800/1*J7pq6EjeQrNJZY5hBKvouA.png align="left")

### Step 5: Selecting an Instance Type

* Choose an instance type. We recommend starting with the “t2.micro” instance type, which is often eligible for the AWS Free Tier. Ensure you choose an instance type that aligns with your specific requirements.
    

![](https://cdn-images-1.medium.com/max/800/1*hnxK13LBUfPl0NFX7uq68w.png align="left")

### Step 6: Creating a Key Pair

* Create a new key pair or choose an existing one. Key pairs are used for securely connecting to your instance. In this example, we’ll create a new key pair. Make sure to download the private key file (.pem) and keep it in a secure location.
    

![](https://cdn-images-1.medium.com/max/800/1*eWrSALUgS9gA4i_nF2mzAw.png align="left")

### Step 7: Configuring Security Groups

* Configure security groups to control inbound and outbound traffic. For this example:
    
* Allow inbound traffic for HTTP (port 80) and HTTPS (port 443) from anywhere. This enables web access to your instance.
    
* Allow inbound SSH (port 22) traffic from “My IP” only. This restricts SSH access to your IP address, enhancing security.
    

![](https://cdn-images-1.medium.com/max/800/1*upvxwkULelbsePZ-LZsS0w.png align="left")

### Step 8: Adding Storage

* Add storage to your instance. You can specify the size and type of the root volume. In this example, we’ll use the default settings, which include a 20 GB General Purpose (SSD) volume.
    

![](https://cdn-images-1.medium.com/max/800/1*PmmXwxiJF2n1kVS15R7qog.png align="left")

### Step 9: Review and Launch

* Review your instance configuration to ensure everything is as desired. Click “Launch” when you’re ready to proceed.
    

![](https://cdn-images-1.medium.com/max/800/1*cTWNGrmt-49W0tp8J2Mt8A.png align="left")

### Step 10: Connecting to Your EC2 Instance via SSH

> Note: To connect to your EC2 instance using SSH, you’ll need Windows Subsystem for Linux (WSL) installed on your Windows machine. If WSL is not installed, you can visit the [WSL Microsoft site](https://docs.microsoft.com/en-us/windows/wsl/install) for installation instructions. Alternatively, you can use PuTTY or other SSH clients, which we can cover in another guide.

* Once your instance is launched, open your WSL terminal and use the SSH command to connect.
    

```java
chmod 400 your-key-pair.pem
ssh -i path-to-your-key-pair.pem ec2-user@your-instance-public-ip
```

![](https://cdn-images-1.medium.com/max/800/1*gfgPplK34jsRjUFt8oCgQA.png align="left")

### Step 11: Creating an HTML File

* After successfully connecting to your EC2 instance, create an HTML file using the following commands:
    

```java
echo "Anil Gulati" > index.html
```

### Step 12: Serving the HTML File

* To make the HTML file accessible over the internet, you can use a simple Python HTTP server. Run the following command:
    

```java
python3 -m http.server 80 &
```

![](https://cdn-images-1.medium.com/max/800/1*Cr4uyG7Lzp4mHC8rX3oHEA.png align="left")

Now, you can access the HTML file by entering your EC2 instance’s public IP address in a web browser.

![](https://cdn-images-1.medium.com/max/800/1*U48CP7PkJXUoPm9akzNEeA.png align="left")

Congratulations! You’ve successfully launched your first Amazon EC2 instance, created an HTML file, and made it accessible online. You’ve taken the first steps towards hosting web content in the cloud. Happy cloud computing!

### Conclusion

Amazon EC2 provides the flexibility and scalability needed to run applications and services in the cloud. By following these steps, you’ve taken your first leap into the world of AWS, setting up a Linux instance, creating web content, and making it available online. Continue your AWS journey with further exploration of EC2 and other AWS services.

### **Enjoyed This Article?**

> ***If you enjoy reading this post, got help, knowledge through it, and want to support my efforts please clap this article and follow.  
> To explore more of my work, visit my portfolio at*** [***anilgulati.tech***](http://anilgulati.tech?utmSource=hashnode&article=AWS-ec2&h=true)