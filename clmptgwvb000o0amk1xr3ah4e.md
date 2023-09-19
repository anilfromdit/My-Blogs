---
title: "Mastering Network Security: A Comprehensive Guide to Amazon VPC in AWS"
seoTitle: "Mastering Network Security: A Comprehensive Guide to Amazon VPC in AWS"
seoDescription: "Learn Amazon VPC essentials, create subnets, and connect to the internet for secure AWS networking."
datePublished: Tue Sep 19 2023 04:30:09 GMT+0000 (Coordinated Universal Time)
cuid: clmptgwvb000o0amk1xr3ah4e
slug: mastering-network-security-a-comprehensive-guide-to-amazon-vpc-in-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694873827229/332059c8-9dc7-4dc1-b437-381830f20f44.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1694874015063/d9dc7119-0a7f-4861-aa7d-db5eaeae13c3.png
tags: cloud, aws, networking, vpc, vpc-peering

---

![](https://cdn-images-1.medium.com/max/800/1*BuZ7po9jRBMftzVV_9-lMw.png align="center")

### Introduction

Amazon Virtual Private Cloud (Amazon VPC) is a fundamental service in Amazon Web Services (AWS) that allows users to create secure and isolated networks within the AWS cloud. In this article, we will explore the key concepts of Amazon VPC and learn how to set up a VPC, subnets, and an EC2 instance within it. By the end of this guide, you will have a clear understanding of how to create your own private network in AWS.

### Chapter 1: VPC Fundamentals

When working with AWS, it’s essential to understand the distinction between configuring VPC settings and adjusting inbound rules. While both are crucial for network security, they serve different purposes.

#### **VPC Settings vs. Inbound Rules**

* VPC Settings: VPC settings refer to the overall configuration of your virtual private cloud. This includes defining the IP address range, creating subnets, and setting up routing tables. These settings determine the fundamental structure of your network.
    
* Inbound Rules: Inbound rules, on the other hand, deal with security group and network ACL configurations. They control traffic coming into your instances, allowing you to specify which ports and sources are permitted. Inbound rules add a layer of security to your VPC.
    

#### Why Amazon VPC?

**Amazon VPC is a critical component of AWS for several reasons:**

* **Isolation**: VPC allows you to create isolated environments within the AWS cloud. This isolation ensures that your resources are protected from external threats.
    
* **Customization**: With VPC, you have full control over your network design. You can create multiple subnets, define IP address ranges, and configure routing as per your requirements.
    
* **Security**: VPC provides robust security features, including security groups and network ACLs, to protect your instances from unauthorized access.
    
* **Connectivity**: VPC allows you to establish secure connections between your on-premises data centres and your AWS resources.
    

#### VPC vs. Private vs. Public Networks

In AWS, networks fall into one of three categories: VPC, private, and public networks.

* **Amazon VPC**: A VPC is a user-defined network within AWS. It provides full control over network settings, making it suitable for hosting applications and services that require isolation and security.
    
* **Private Network:** A private network refers to a network segment that is not directly accessible from the Internet. Resources within a private network can communicate with each other but are shielded from external traffic.
    
* **Public Network**: A public network is directly accessible from the internet. Resources in a public network can send and receive data from the internet, making them suitable for web servers and publicly accessible applications.
    

### Chapter 2: Creating Your VPC

In this chapter, we’ll walk you through the process of creating your own Amazon VPC. Before we dive into the practical steps, let’s clarify some fundamental concepts.

#### Understanding CIDR Notation

CIDR, or Classless Inter-Domain Routing, notation is used to define the IP address range for your VPC. It consists of an IP address and a prefix length, separated by a slash (“/”). For example, “10.0.0.0/16” represents an IP address range from 10.0.0.0 to 10.0.255.255, with a total of 65,536 IP addresses. The prefix length (in this case, “/16”) determines the size of the IP address block.

#### Creating Your Amazon VPC

![](https://cdn-images-1.medium.com/max/800/1*bsOBRoK67Fl6ais39TysoQ.png align="left")

1. Log in to your AWS Management Console: Ensure that you’re logged in to your AWS account.
    
2. Open the VPC Dashboard: From the AWS Management Console, navigate to the “Services” menu and select “VPC” under the “Networking & Content Delivery” section.
    
3. Start VPC Wizard: In the VPC Dashboard, click on the Create VPC ” button to initiate the VPC creation process.
    
4. Select a VPC Configuration: The VPC Wizard offers various configuration options. For beginners, the “VPC with a Single Public Subnet” configuration is a good starting point. It sets up a VPC with one public subnet.  
    

![](https://cdn-images-1.medium.com/max/800/1*pkBZnhdYnp05-_vMXRv7Gw.png align="left")

**Configure Your VPC:**

* **IPv4 CIDR Block:** Define the IP address range for your VPC using CIDR notation. For instance, you can use “10.0.0.0/16” for a large address range.
    
* **VPC Name**: Give your VPC a descriptive name to help identify it later.
    
* **Public Subnet:** Specify the IP address range for the public subnet, usually a subset of the VPC’s address range. For example, if your VPC is “10.0.0.0/16,” your public subnet could be “10.0.0.0/24.”
    

5. **Create a VPC**: After configuring the details, click the “Create VPC” button. AWS will now create your VPC based on the chosen configuration.

Confirmation: Once the VPC creation process is complete, you’ll see a confirmation message. Note down the VPC ID for reference.

![](https://cdn-images-1.medium.com/max/800/1*OCQNosBlY1nVHarfpbX7mQ.png align="left")

> Congratulations! You’ve successfully created your Amazon VPC. Now let’s move on to the next step: creating subnets within your VPC.

### Chapter 3: Creating Subnets in Your VPC

Now that you’ve established your Amazon VPC, it’s time to carve it up into smaller, manageable segments known as subnets. Subnets allow you to organize your resources, control traffic flow, and enhance security within your VPC.

#### Why Use Subnets in Your VPC

* **Traffic Isolation**: Subnets help isolate different types of traffic. For example, you can have public subnets for resources that need direct internet access and private subnets for sensitive databases or backend services.
    
* **Security Group Control**: Security groups are applied at the subnet level. By placing resources in specific subnets, you can enforce different security policies for different types of resources.
    
* **Availability Zone (AZ) Placement**: Subnets are associated with specific AZs. Distributing your resources across multiple AZs and subnets enhances high availability and fault tolerance.
    

#### Creating Subnets

1. **Select Your VPC**: In the VPC Dashboard, locate the VPC you created in Chapter 2. Click on it to select it.
    
2. **Create Subnet**: With your VPC selected, click on the “Subnets” tab, and then click the “Create Subnet” button.
    

![](https://cdn-images-1.medium.com/max/800/1*et0agFitehwklr36b-_7Qw.png align="left")

3\. **Define Subnet Details**:

* Name: Give your subnet a meaningful name, like “Public Subnet 1” or “Private Subnet 2.”
    
* VPC: Ensure your VPC is selected.
    
* Availability Zone: Choose an AZ for your subnet. You can create subnets in different AZs to distribute resources for high availability.
    
* IPv4 CIDR Block: Specify the IP address range for this subnet. It should be a subset of your VPC’s CIDR block. For example, if your VPC is “10.0.0.0/16,” your subnet could be “10.0.1.0/24.”
    

![](https://cdn-images-1.medium.com/max/800/1*o3nljB4NaQO3F8PgbJkRCA.png align="left")

![](https://cdn-images-1.medium.com/max/800/1*BGuwTGMToAIVzPCR6lrzyw.png align="left")

4\. **Configure Route Table**: Associate your subnet with a route table. If you’re creating a public subnet for resources that need internet access, choose the main route table or a custom route table that routes traffic to an Internet Gateway (IGW).

5. **Create the Subnet**: Click the “Create Subnet” button to create the subnet.

6\. **Repeat as Needed**: Depending on your requirements, you can create multiple subnets in different AZs with distinct CIDR blocks.

7\. **Confirmation**: Once the subnet is created, you’ll see it listed in the Subnets tab. Note down the subnet ID for future reference.

![](https://cdn-images-1.medium.com/max/800/1*7Aiq8oLmHDdHv15YjgFmEA.png align="left")

> Great job! You’ve successfully created subnets within your Amazon VPC, laying the foundation for building a robust and well-organized network infrastructure.

### Chapter 4: Launching an EC2 Instance in Your VPC

Now that you’ve created subnets within your Amazon VPC, it’s time to put them to use by launching an Amazon Elastic Compute Cloud (EC2) instance. EC2 instances are virtual servers in the cloud that you can use to run applications and services.

#### Why Use EC2 Instances in Your VPC

* **Scalability**: EC2 instances can be easily scaled up or down to accommodate changes in demand for your applications.
    
* **Customization**: You have full control over the operating system, software, and configurations of your EC2 instances.
    
* **Diverse Workloads:** EC2 instances are versatile and can handle a wide range of workloads, from web hosting to data processing.
    

#### Launching an EC2 Instance

1. **Access the EC2 Dashboard:** Log in to your AWS Management Console, open the “Services” menu, and select “EC2” under “Compute.”
    
2. **Launch Instance:** In the EC2 Dashboard, click the “Instances” link in the left navigation pane, and then click the “Launch Instance” button.
    

![](https://cdn-images-1.medium.com/max/800/1*Z_GZDtn8ixHv4nSo81vvkA.png align="left")

**3\. Choose an Amazon Machine Image (AMI):** Select an AMI based on your requirements. For this tutorial, you can use the “Ubuntu” which is a free, stable, and well-supported choice.

**4\. Choose an Instance Type**: Select the instance type that matches your workload. The t2.micro instance is eligible for the AWS Free Tier and is suitable for testing.

1. **Configure Instance Details**:
    

* Number of Instances: Set the number of instances you want to launch (usually 1).
    
* Network: Choose the VPC you created in Chapter 1.
    
* Subnet: Select one of the subnets you created in Chapter 3.
    
* Auto-assign Public IP: If you want your instance to have a public IP address, set this option to “Enable.”
    

![](https://cdn-images-1.medium.com/max/800/1*69UgIe7orRZAUTSdi8GJ1w.png align="left")

1. Add Storage: Specify the amount of storage you need for your instance. The default settings should be sufficient for this tutorial.
    
2. Add Tags (Optional): You can add key-value tags to your instance for better organization and identification.
    
3. Configure Security Group: Create a new security group or use an existing one. Make sure it allows inbound traffic on the ports your applications will use (e.g., port 80 for HTTP).
    
4. Review and Launch: Review your instance configuration, and then click the “Launch” button.
    
5. Select Key Pair: Choose an existing key pair or create a new one. This key pair is crucial for SSH access to your instance.
    
6. Launch Instances: Click the “Launch Instances” button to launch your EC2 instance.
    
7. Confirmation: You’ll see a confirmation screen with a success message. Click the “View Instances” button to go back to the Instances Dashboard.
    

![](https://cdn-images-1.medium.com/max/800/1*1kdAtw1AFa8JQAZLWXWZuw.png align="left")

> Note: You Won’t be able to Connect To The Instance right now

![](https://cdn-images-1.medium.com/max/800/1*mfRv76XSKorJN1b_AVe5nQ.png align="left")

> Congratulations! You’ve successfully created an EC2 instance within your Amazon VPC. This instance is now part of your virtual private network 

### Chapter 5: Connecting Your VPC to the Internet

In the previous chapters, we created a Virtual Private Cloud (VPC), and launched an Amazon EC2 instance within it. Now, let’s explore how to connect your VPC to the internet, allowing your instances to communicate with the outside world.

#### 1\. Internet Gateway Creation

![](https://cdn-images-1.medium.com/max/800/1*WIsZzbu1Wr8reRegiJxjlA.png align="left")

First, we need to create an internet gateway, which acts as a gateway for traffic between your VPC and the internet.  

* Open the AWS Management Console.
    
* Navigate to the VPC Dashboard.
    
* Select “Internet Gateways” from the left sidebar.
    
* Click “Create Internet Gateway.”
    

![](https://cdn-images-1.medium.com/max/800/1*FVff1k-uMuwANJOW4ax_SQ.png align="left")

* Provide a name for your gateway (e.g., “myBlogVpcInternetGateway”) and click “Create Internet Gateway.”
    

2. **Attach the Internet Gateway to Your VPC**

Next, we’ll attach the internet gateway to your VPC.

* Select the internet gateway you just created.
    
* From the “Actions” menu, choose “Attach to VPC.”
    

![](https://cdn-images-1.medium.com/max/800/1*9n-2EtlqViu03V2dB-64JA.png align="left")

![](https://cdn-images-1.medium.com/max/800/1*5Rp7C3ya0kAaY2taFSGJjw.png align="left")

* Select your VPC and click “Attach Internet Gateway”
    

3\. **Update Route Table**

To direct internet-bound traffic from your instances to the internet gateway, update your VPC’s route table.

* In the VPC Dashboard, choose “Route Tables” from the left sidebar.
    

![](https://cdn-images-1.medium.com/max/800/1*UIFsLiDOy_n1-8MMiSj9Aw.png align="left")

* Select the route table associated with your public subnet (if you don’t have one, create a new route table).
    
* In the “Routes” tab, click “Edit routes.”
    

![](https://cdn-images-1.medium.com/max/800/1*MSxcbeCVlUtrTPKrzdScrg.png align="left")

* Add a new route with destination “0.0.0.0/0” and target as the internet gateway you attached in the previous step.
    

![](https://cdn-images-1.medium.com/max/800/1*SyTAZp9JwXKZ1zX6eAsQsg.png align="left")

* Save the route table.
    

**4\. Test Connectivity**

Now that your VPC is connected to the internet, test the connectivity of your EC2 instance. You should be able to SSH into the instance or access any public services running on it.

![](https://cdn-images-1.medium.com/max/800/1*hZ1UFNz3ElANFwyG5bFdbQ.png align="left")

**Benefits of Connecting Your VPC to the Internet:**

* Allows your EC2 instances to access external resources, such as databases, APIs, or software repositories.
    
* Enables hosting public-facing web applications and services.
    
* Streamlines software updates and package installations via the internet.
    

#### Considerations:

* Ensure that your security group rules and NACL rules are configured correctly to maintain a secure environment.
    
* Monitor your internet data transfer costs, especially if you have significant outbound traffic.
    

> With your VPC now connected to the internet, your EC2 instances can communicate externally. In the upcoming chapter, we will cover private and public subnets connected to EC2 instances and how they can communicate with each other without being connected to the outer internet.

### Enjoyed This Article?

> *If you enjoy reading this post, got help, knowledge through it, and want to support my efforts please clap this article and follow.  
> To explore more of my work, visit my portfolio at* [*anilgulati.tech*](http://anilgulati.tech?utmSource=hashnode&article=AWS-VPC-1)