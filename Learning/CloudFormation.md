````markdown
# 🏗️ AWS CloudFormation (CFT)

CloudFormation is an **Infrastructure as Code (IaC)** tool **exclusive to AWS** that enables you to provision AWS infrastructure using **declarative templates** written in **YAML** or **JSON**.

---

## 📘 What is CloudFormation?

- A **template-based** tool to define and manage AWS resources.
- Implements **IaC (Infrastructure as Code)** — unlike AWS CLI, which is procedural.
- Allows **declarative, repeatable**, and **version-controlled** infrastructure deployment.
- Converts the file (YAML/JSON) into **API calls** to AWS for resource creation.

---

## 🛠️ When to Use

| Use Case              | Tool         |
|-----------------------|--------------|
| Quick actions         | AWS CLI      |
| Creating full stacks  | CloudFormation |

Use **CloudFormation** when you want to provision **multiple resources or full environments** (e.g., VPC, EC2, S3, etc.).

---

## ⭐ Key Features

- 📦 Create complex infrastructure in stacks
- 🔁 Reusability via templates
- 🔍 Drift Detection (identify changes made outside CFT)
- ✅ Automated rollback and change sets
- 🧩 Supported in **Visual Studio Code** with extensions

---

## 🧾 Sample CloudFormation Template (YAML)

```yaml
AWSTemplateFormatVersion: "2010-09-09"
Description: A sample CloudFormation template

Resources:
  MyEC2Instance: # Inline comment
    Type: "AWS::EC2::Instance"
    Properties:
      ImageId: "ami-0ff34564"
      InstanceType: "t2.micro"
      KeyName: "testkey"
      BlockDeviceMappings:
        - DeviceName: "/dev/sdm"
          Ebs:
            VolumeType: "io1"
            Iops: 200
            DeleteOnTermination: false
            VolumeSize: 20
````

---

## 🪣 Sample S3 Bucket Resource

```yaml
Resources:
  S3Bucket:
    Type: "AWS::S3::Bucket"
    Properties:
      BucketName: "demo.aws.sss.example.com"
```

---

## 🚀 How to Deploy a Template

1. Go to **AWS Console**
2. In search bar, type **"CloudFormation"** and open it
3. Click on **Stacks → Create Stack**
4. Choose **"Template is ready"**
5. Upload your YAML template file (e.g., `s3.yaml`)
6. Submit

✅ AWS will create the resources as defined in the template.

---

## 🔧 Tools and Extensions

* 🧩 **VS Code Plugins for CFT**:

  * **YAML** by RedHat
  * **AWS Toolkit** for code completion and deployment

---

## 🌍 Terraform vs CloudFormation

| Feature             | CloudFormation | Terraform |
| ------------------- | -------------- | --------- |
| AWS only            | ✅ Yes          | ❌ No      |
| Multi-cloud support | ❌ No           | ✅ Yes     |
| Language            | YAML / JSON    | HCL       |
| Native AWS support  | ✅ Yes          | ✅ Yes     |



