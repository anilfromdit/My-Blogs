---
title: "Introduction to AWS and IAM Basics: A Comprehensive Guide to AWS Security"
seoTitle: "Introduction to AWS and IAM: A Comprehensive Guide to AWS Security"
seoDescription: "Learn how to create IAM users, boost AWS security, and implement best practices. Strengthen your cloud defences"
datePublished: Sat Sep 16 2023 04:30:09 GMT+0000 (Coordinated Universal Time)
cuid: clmlj5cpf000l09l0emotfhw3
slug: introduction-to-aws-and-iam-basics-a-comprehensive-guide-to-aws-security
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694815011481/d98d13fd-17c1-472c-a7d9-65f0bb7ab0a7.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1694815488526/3c7c212e-3fa7-475b-9f56-1713b4c13fa0.png
tags: cloud, aws, security, best-practices, aws-iam

---

Amazon Web Services (AWS) has transformed the way organizations operate in the digital age. It offers a secure, scalable, and flexible cloud computing platform that empowers businesses to build, deploy, and manage applications and services with ease. However, this vast landscape of cloud resources and services also brings an increased need for robust security mechanisms. This is where AWS Identity and Access Management (IAM) comes into play, serving as the linchpin of AWS security.

### Logging in to AWS: The Importance of IAM Over Root Credentials

When you create an AWS account, you’re provided with root user credentials. These credentials grant unrestricted access to all AWS resources and services. While it may seem convenient to use root credentials for all your activities, it’s essential to understand why this is strongly discouraged:

### 1\. Security Risk

The root user has the highest level of privilege within your AWS account. Using root credentials for routine tasks exposes you to a significant security risk. A simple mistake or unauthorized access can lead to severe consequences, including data breaches and financial losses.

### 2\. Lack of Audit Trail

Actions performed using root credentials make it challenging to track who did what within your AWS account. In contrast, IAM users leave a clear audit trail of their activities, enhancing accountability and making it easier to investigate any suspicious actions.

![](https://cdn-images-1.medium.com/max/1000/0*mY7uvIcbKtMAGR9O align="left")

### 3\. Least Privilege Principle

IAM enables you to adhere to the principle of least privilege. This means granting only the minimum level of access necessary for users to perform their tasks. Root user access is an all-or-nothing proposition, making it difficult to follow this security best practice.

Now that we’ve emphasized the importance of IAM let’s delve into the step-by-step process of creating an IAM user and assigning appropriate permissions.

### Step-by-Step Guide to Creating an IAM User

![AWS IAM logo](https://cdn-images-1.medium.com/max/1000/1*O-odp5nJokAq5FX9VmL9Ew.png align="left")

### Step 1: Access the AWS Management Console

1. Open your web browser and navigate to the [AWS Management Console](https://aws.amazon.com/console/).
    
2. Sign in using your AWS account credentials. Ensure that you have administrative privileges or the necessary permissions to create IAM users.
    

![AWS login Page](https://cdn-images-1.medium.com/max/1000/1*XxQPCFz6IYGzy0stZqR0aA.png align="left")

AWS login Page

### Step 2: Navigate to the IAM Dashboard

1. Once you’re logged in, click on the “Services” menu in the upper-left corner, and then type “IAM” into the search bar. Click on “IAM” under the “Security, Identity, & Compliance” section.
    

![IAM Dashboard](https://cdn-images-1.medium.com/max/1000/1*a3EiMGZYYBOJoFVmfxYIvw.png align="left")

IAM Dashboard

### Step 3: Create a New IAM User

1. In the IAM dashboard, select “Users” from the left-hand navigation pane.
    

![](https://cdn-images-1.medium.com/max/1000/1*oZFgFP0EK_DKSjrSDSQLbA.png align="left")

2\. Click the “Create user” button to initiate the process of creating a new IAM user.

![](https://cdn-images-1.medium.com/max/1000/1*bZhjsoLpNDR66rgEK9WLEQ.png align="left")

### Step 4: Configure User Details

1. In the “User details” section, provide a username for the new IAM user. This username will serve as the user’s identity for authentication when accessing AWS resources.  
    

![](https://cdn-images-1.medium.com/max/1000/1*HcRRbTfD5RyS0gUbp5C-QA.png align="left")

### Step 5: Set Permissions

1. In the “Set permissions” section, you can assign permissions to the IAM user. You have several options:
    

> Add user to the group: Assign the user to an existing IAM group that already has predefined permissions.

> Attach existing policies directly: Attach one or more AWS-managed policies or customer-managed policies to the user. These policies define what actions the user can perform within AWS.

> Add user to group and attach policies: Combine the group-based and policy-based permission assignments for greater flexibility.

![](https://cdn-images-1.medium.com/max/1000/1*T7GWaOMntH5w-wLTyWJajg.png align="left")

2\. Choose the appropriate permissions based on your organization’s requirements Here in this article we’re giving EC2 full Access. Be mindful of the principle of least privilege, granting only the necessary access for the user’s specific tasks.  

### Step 6: Configure Tags (Optional)

1. You have the option to add tags to the IAM user for better organization and resource management. Tags are key-value pairs that help you categorize and track users efficiently.
    

![](https://cdn-images-1.medium.com/max/1000/1*1R44lbrkMEEMPX_HYg8flA.png align="left")

### Step 7: Review and Create User

1. Carefully review the user’s details, permissions, and tags to ensure they are accurate.
    
2. Once you’re satisfied with the configuration, click the “Create user” button.
    

![](https://cdn-images-1.medium.com/max/1000/1*QIqdXjQ7I_EFO3GZ6S2jLw.png align="left")

### Step 8: Access User Credentials

1. The IAM user has been created successfully. Let’s enable console access
    

![](https://cdn-images-1.medium.com/max/1000/1*IxApfvi_wPuX1TgtlTrs3g.png align="left")

![](https://cdn-images-1.medium.com/max/1000/1*I8RisbuWO4La8UVJPFKDZw.png align="left")

![](https://cdn-images-1.medium.com/max/1000/1*yBNE-2OKG4Vod4BQFmoLdg.png align="left")

### Multi-Factor Authentication (MFA) for Added Security

Before we conclude, it’s essential to mention an additional layer of security: Multi-Factor Authentication (MFA). MFA adds an extra barrier to unauthorized access by requiring users to provide two or more separate authentication factors.

To enhance the security of your IAM users, consider enabling MFA. This involves linking a physical device (like a smartphone) or a virtual MFA app (e.g., Google Authenticator) to the IAM user account. When users sign in, they must provide not only their password but also a one-time authentication code generated by the MFA device.

MFA significantly reduces the risk of unauthorized access, even if a malicious actor obtains a user’s password. It’s a highly recommended security practice when managing AWS resources.

### Tasks Only the Root User Can Perform

While it’s crucial to limit the use of root user credentials, there are certain tasks that only the root user can undertake. These include:

* Closing the AWS Account: Initiating the closure of your AWS account can only be performed by the root user.
    
* Managing Billing and Payment Information: Updating billing and payment settings, as well as changing the AWS support plan, is the responsibility of the root user.
    
* Recovering a Compromised Account: In the unfortunate event of an account compromise, the root user is essential for regaining control and securing the account.
    

In summary, creating and utilizing IAM users is a fundamental practice in AWS that enhances security, accountability, and control over your AWS resources. While the root user provides ultimate access, it should be reserved for critical administrative tasks. IAM users should serve as the primary method for interacting with AWS resources in a secure and manageable manner. By following these best practices, including enabling MFA, you’ll strengthen your AWS security posture and minimize potential risks.  
  
**Enjoyed This Article?**

> ***If you enjoy reading this post, got help, knowledge through it, and want to support my efforts please clap this article and follow.  
> To explore more of my work, visit my portfolio at*** [***anilgulati.tech***](http://anilgulati.tech?utmSource=hashnode&article=AWS-IAM&r=true)