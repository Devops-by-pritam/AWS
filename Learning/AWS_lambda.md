
#  AWS Lambda - Simplified Guide

##  What is AWS Lambda?

AWS Lambda is a **serverless compute service** that runs your code **in response to events** and **automatically manages the compute resources** for you.

### Key Highlights:
- **Event-driven:** Code is triggered by events like S3 uploads, DynamoDB updates, API Gateway calls, etc.
- **No server management:** You don't need to provision or manage servers.
- **Cost optimization:** You pay only for the compute time you consume.
- **Security & Compliance:** Helps enforce policies for example, alerting when disallowed resources are used.

---

##  Use Case Example

Suppose your organization has a compliance rule that certain AWS resources **must not be used**. If a developer mistakenly creates such a resource, Lambda can **detect and alert** using EventBridge (CloudWatch Events) + SNS.

---

##   How to Create a Lambda Function

### 1. Go to AWS Console â†’ Lambda Service

### 2. Click `Create function`

- Choose **Author from scratch**
- Enter:
  - **Function name** (e.g., `CheckDisallowedResources`)
  - **Runtime** (e.g., Python, Node.js)
- Click **Create Function**

### 3. Write Your Code

In the inline editor or upload from a ZIP/S3.

Make sure the function has a **handler**, typically like:

```python
def lambda_handler(event, context):
    print("Lambda triggered!")
    # Your logic here
```

>  You can change the handler name later in the **Configuration > General configuration** section.

### 4. Set Permissions (IAM Role)

- Attach or create an IAM role with **permissions to access other AWS services** your function interacts with.
    - Example: S3, CloudWatch, SNS, DynamoDB, etc.

>  Without proper permissions, Lambda won't be able to talk to other services.

---

##  Notification Example (Security/Compliance)

- Use CloudTrail or EventBridge to capture events like resource creation.
- Trigger a Lambda function on such events.
- Lambda checks if the resource violates rules.
- If yes, use **SNS** or **Email** to send alerts.

---

## Summary

AWS Lambda is **powerful**, **scalable**, and **cost-effective**. It's great for:
- Automating tasks
- Monitoring resources
- Enforcing compliance
- Building APIs and backend services

---

