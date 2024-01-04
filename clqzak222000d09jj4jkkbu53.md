---
title: "Stop /Start AWS EC2  at regular intervals"
seoTitle: "Start Stop AWS EC2  at regular intervals"
seoDescription: "automate ec2 instance"
datePublished: Thu Jan 04 2024 14:17:14 GMT+0000 (Coordinated Universal Time)
cuid: clqzak222000d09jj4jkkbu53
slug: stop-start-aws-ec2-at-regular-intervals
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/K-Iog-Bqf8E/upload/41452ecc39af6faca547739681dd840d.jpeg
tags: lambda, cloud, ec2, aws, developer, cloud-computing, devops, devsecops

---

# AWS Cloud

As organizations scale their **cloud infrastructure** on Amazon Web Services (AWS), the cost of running instances can become a significant concern. Many workloads do not require 24/7 availability, leading to unnecessary expenses. Fortunately, AWS offers a simple and effective solution to address this issue, using **AWS Lambda** to automate the start and stop processes of **EC2** instances at regular intervals.

In this blog post, we will explore the benefits of automating EC2 instances and demonstrate how to implement this cost optimization strategy using **AWS Lambda**.

## **Benefits of Automating EC2 Instances**

1. **Cost Savings:** By stopping non-critical EC2 instances when they are not in use, organizations can significantly reduce their cloud infrastructure costs. AWS charges on a pay-as-you-go model, which means that instances running 24/7 can lead to higher bills. Automating the start and stop process allows you to pay only for the compute resources you genuinely need.
    
2. **Environment Friendly:** Implementing EC2 instance automation promotes sustainable practices by reducing the overall carbon footprint. Unnecessary instances that consume energy can be turned off, resulting in a greener and more eco-friendly cloud infrastructure.
    
3. **Enhanced Security:** Stopping instances when they are not needed can minimize the attack surface and potential security risks. It is a proactive approach to limit exposure to the public internet during periods of inactivity.
    
4. **Simplified Management:** Automating the start and stop of EC2 instances frees up valuable time for your IT team. Manual intervention to manage instance uptime can be a time-consuming task, and automation reduces the burden of administrative work.
    

> *Note: The following resolution is a simple solution. For a more robust solution, use the AWS Instance Scheduler. For more information, see* [*Automate starting and stopping AWS instances*](https://docs.aws.amazon.com/solutions/latest/instance-scheduler-on-aws/welcome.html)*.*

---

**Let's Begin ✌️**

**Step 1: Create a custom AWS IAM policy**

**Step 2: Create an IAM role for Lambda**

**Step 3: Create Lambda functions that stop and start your EC2**

**Step 4: Test your Lambda functions**

**Step 5: Create EventBridge rules that trigger your function on a schedule**

Note: You can also [create rules that trigger on an event that takes place in your AWS account](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-create-rule.html).

## **Step 1: Create an IAM policy and execution role for your Lambda function:**

1\. Login into the **AWS Console**. And go to **IAM** Config

2\. [Create an IAM policy using the JSON policy editor](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html#access_policies_create-json-editor). Copy and paste the following JSON policy document into the policy editor:

![](https://miro.medium.com/v2/resize:fit:875/1*RAL5pqHthL4IH5SitT5QNw.png align="left")

```bash
{
"Version": "2012–10–17",
"Statement": [
{
"Effect": "Allow",
"Action": [
"logs:CreateLogGroup",
"logs:CreateLogStream",
"logs:PutLogEvents"
],
"Resource": "arn:aws:logs:*:*:*"
},
{
"Effect": "Allow",
"Action": [
"ec2:Start*",
"ec2:Stop*"
],
"Resource": "*"
}
]
}
```

## **Step 2:**[**Create an IAM role**](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html#roles-creatingrole-service-console) **for Lambda:**

![](https://miro.medium.com/v2/resize:fit:875/1*XLWhPDQezFdpRzqDnygdmw.png align="left")

1\. In the navigation pane of the IAM console, choose **Roles**, and then choose **Create role**.

2\. For **Select trusted entity**, choose **AWS service**.

> ***Important:*** *When attaching a permissions policy to Lambda, make sure that you choose the IAM policy that you just created.*

3\. Now Select Policy Previously we created

![](https://miro.medium.com/v2/resize:fit:875/1*YkD2uL5KZRHoD-bi9X6aqQ.png align="left")

## **Step 3: Create Lambda functions that stop and start your EC2 instances:**

1\. In the [Lambda console](https://console.aws.amazon.com/lambda/), choose **Create** function.

2\. Choose **Author from scratch**.

3\. Under Basic information,

Add the following:  
For **Function name**, enter a name that identifies it as the function used to stop your EC2 instances. For example, “**StopEC2Instances**”.  
For **Runtime**, choose **Python 3.9**.  
Under **Permissions**, expand Change default execution role.  
Under **Execution role**, choose **Use an existing role**.  
Under **Existing role**, choose the IAM role that you created.

4\. Choose **Create function**.

5\. Under **Code**, Code source, copy and paste the following code into the [editor pane in the code editor](https://docs.aws.amazon.com/lambda/latest/dg/foundation-console.html#code-editor) (lambda\_function). This code stops the EC2 instances that you identify.

6.Check you **Instance IDs** and **Region** and change to the below config

```bash
import boto3
region = 'ap-south-1'
instances = ['i-12345cb6de4f78g9h', 'i-08ce9b2d7eccf6d26']
ec2 = boto3.client('ec2', region_name=region)
def lambda_handler(event, context):
ec2.stop_instances(InstanceIds=instances)
print('stopped your instances: ' + str(instances))
```

**( Code as case sensitive and it will prompt error for Extra space )**

> ***Important:*** *For* ***region****, replace “ap-south-1” with the AWS Region that your instances are in. For instances, replace the example EC2 instance IDs with the IDs of the specific instances that you want to stop and start.*

6\. Choose **Deploy**.

![](https://miro.medium.com/v2/resize:fit:875/1*3neukqGBWC6gfMNpiH3IJA.png align="left")

7\. On the **Configuration** tab, choose **General configuration**, Edit. Set Timeout to **10** seconds and then select **Save**.

> ***Note:*** [*Configure the Lambda function settings*](https://docs.aws.amazon.com/lambda/latest/dg/resource-model.html) *as needed for your use case. For example, if you want to stop and start multiple instances, you might need a different value for Timeout and Memory.*

![](https://miro.medium.com/v2/resize:fit:875/1*cckyQYOFPlYIBYjRq4rkyw.png align="left")

8\. Repeat steps 1–7 to create another function. Do the following differently so that this function starts your EC2 instances:

In step 3, enter a different **Function name** than the one you used before. For example, “**StartEC2Instances**”.  
In step 5, copy and paste the following code into the editor pane in the code editor (lambda\_function):

Example function code — starting EC2 instances

```bash
import boto3
region = 'ap-south-1'
instances = ['i-12345cb6de4f78g9h', 'i-08ce9b2d7eccf6d26']
ec2 = boto3.client('ec2', region_name=region)
def lambda_handler(event, context):
ec2.start_instances(InstanceIds=instances)
print('started your instances: ' + str(instances))
```

**( Code as case sensitive and it will prompt error for Extra space )**

> ***Important:*** *For region and instances , use the same values that you used for the code to stop your EC2 instances.*

## **Step 4: Test your Lambda functions:**

1\. In the [Lambda console](https://console.aws.amazon.com/lambda/home), choose **Functions**.

2\. Choose one of the functions that you created.

3\. Select the **Code** tab.

4\. In the Code source section, select **Test**.

5\. In the Configure test event dialog box, choose **Create new test event**.

6\. Enter an **Event name**. Then, choose **Create**.

**Note:** You don’t need to change the JSON code for the test event — the function doesn’t use it.

7\. Choose **Test** to run the function.

8\. Repeat steps 1–6 for the other function that you created (Start Instances).

> *Tip: You can* [*check the status of your EC2 instances*](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-system-instance-status-check.html#viewing_status) *before and after testing to confirm that your functions work as expected.*

## **Step 5: Create EventBridge rules that trigger your Lambda functions:**

1\. Open the [Eventbridge console](https://console.aws.amazon.com/events/).

2\. Select **Create rule.**

3\. Enter a Name for your **rule**, such as **“StopEC2Instances**”. You can optionally enter a Description.

4\. In **Define pattern**, select **Schedule**.

5\. Do either of the following:

> *For Fixed rate of, enter an interval of time in minutes, hours, or days.  
> For Cron expression, enter an expression that tells Lambda when to stop your instances. For information on expression syntax, see* [*Schedule expressions for rules*](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html)*.  
> ****Note:*** *Cron expressions are evaluated in UTC. Make sure that you adjust the expression for your preferred time zone.*

![](https://miro.medium.com/v2/resize:fit:875/1*C3FG602rKnJKrA6nteTPeA.png align="left")

6\. In Select **targets**, choose **Lambda function** from the Target drop-down menu.

7\. For **Function**, choose the function that **stops your EC2 instances**.

8\. Scroll down and then select **Create**.

9\. Repeat steps 1–8 to create a rule to start your EC2 instances. Do the following differently:

Enter a name for your rule, such as “**StartEC2Instances**”.  
(Optional) Enter a Description, such as “Starts EC2 instances every morning at 7 AM.”  
In step 5, for Cron expression, enter an expression that tells Lambda when to start your instances.  
In **step 7**, for Function, choose the function that **starts your EC2 instances**.

---

Follow for More 👉

[![Karthick Dk](https://miro.medium.com/v2/resize:fill:55:55/1*wjjLaOLpOggypEpFfAmu5A.jpeg align="left")](https://www.linkedin.com/in/karthick-dkk/)

Medium — [https://medium.com/@karthidkk123](https://medium.com/@karthidkk123)  
Linked In — [https://www.linkedin.com/in/karthick-dkk/](https://www.linkedin.com/in/karthick-dkk/)  
Instagram — [https://www.instagram.com/karthick\_dkk\_dk/](https://medium.com/new-story?source=---two_column_layout_nav----------------------------------)

[By Me Coffee](https://www.buymeacoffee.com/karthidkk1Q) 👍