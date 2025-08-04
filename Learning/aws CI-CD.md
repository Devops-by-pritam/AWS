🚀 Getting Started with AWS CI/CD 

AWS has its own set of tools to handle the whole CI/CD process — from writing code to deploying it live. Think of it as AWS's in-house DevOps suite.

Here’s how it all connects:

```
+-------------+     +------------+     +-------------+     +-------------+
|  CodeCommit | --> | CodePipeline| --> |  CodeBuild  | --> | CodeDeploy  |
+-------------+     +------------+     +-------------+     +-------------+
   (Source)           (Orchestrator)      (Build/CI)         (Deployment)
```

---

🗃️ CodeCommit — Your Private Git Repo

What it is:

* A private Git-based repository service, like GitHub but inside AWS.

How to use:

1. Go to CodeCommit → Create Repository.
2. IAM role: give yourself `AWSCodeCommitPowerUser` permissions.
3. Set up Git on your machine (if not done):

   ```bash
   git config --global user.name "your-iam-username"
   git config --global credential.helper '!aws codecommit credential-helper $@'
   git config --global credential.UseHttpPath true
   ```
4. Clone and push your code.

Pros:

 Fully private, secure, and within AWS.

Cons:

 UI is basic — not ideal for uploading multiple files.
 Lacks 3rd-party integrations compared to GitHub.

---

 🧩 CodePipeline — The CI/CD Brain

What it does:

* Connects all the dots (source → build → deploy)
* Triggers builds when someone pushes to the repo

Steps:

1. Go to CodePipeline → Create Pipeline.
2. Connect to CodeCommit or GitHub as the source.
3. Choose CodeBuild as the build provider.
4. Add CodeDeploy as the deploy step.
5. Done! Now any code changes will auto-trigger the pipeline.

Visual:

```
[ CodeCommit / GitHub ]
          ↓
     CodePipeline
    /            \
CodeBuild      CodeDeploy
```

---

 🔨 CodeBuild — Your Build/CI Engine

What it is:

 AWS’s CI tool that runs builds and tests in Docker containers.

Steps:

1. Go to CodeBuild → Create Project
2. Source: CodeCommit or GitHub
3. Environment: Managed Ubuntu image
4. Permissions: Attach a service role

buildspec.yml Example:

```yaml
version: 0.2
phases:
  install:
    commands:
      - echo Installing packages...
  build:
    commands:
      - echo Building the app...
```

💡 Pro Tip: Handling Secrets

* Use Systems Manager > Parameter Store
* Create a parameter with type `SecureString`
* Reference it in `buildspec.yml`

---

 🚀 CodeDeploy — The Final Push

What it does:

* Deploys your app to EC2, ECS, or Lambda

Setup:

1. Create EC2 instance
2. Install CodeDeploy agent:

   ```bash
   sudo yum update -y
   sudo yum install ruby wget -y
   cd /home/ec2-user
   wget https://bucket-name.s3.region.amazonaws.com/latest/install
   chmod +x ./install
   sudo ./install auto
   sudo service codedeploy-agent start
   ```
3. IAM:

   * EC2 instance role: `AmazonEC2RoleforAWSCodeDeploy`
   * CodeDeploy service role: `AWSCodeDeployRole`
4. In CodeDeploy:

   * Create application
   * Create deployment group (In-place is enough to learn)

AppSpec Example:

```yaml
version: 0.0
os: linux
files:
  - source: /
    destination: /var/www/html
hooks:
  BeforeInstall:
    - location: scripts/install.sh
      runas: root
```

---

 🆚 Compared to Traditional CI/CD

| Feature                | Traditional (Jenkins, GitHub Actions) | AWS CI/CD (CodeSuite)     |
| ---------------------- | ------------------------------------- | ------------------------- |
| Setup Complexity       | Manual setup + host maintenance       | Mostly managed            |
| UI/UX                  | Depends on tools                      | Integrated in AWS Console |
| Pricing                | Can be free (Jenkins) or costly       | Pay-as-you-go             |
| 3rd-party Integrations | Strong (Slack, Trello, etc.)          | Limited outside AWS       |
| Vendor Lock-in         | Low                                   | High (AWS-specific)       |

👍 Pros of AWS CI/CD:

* All managed services
* Tight integration with AWS IAM and infra
* Minimal maintenance

👎 Cons:

* Less flexible UI
* AWS-only ecosystem
* Slight learning curve with IAM

---

If you're already in AWS — using EC2, S3, Lambda, etc. — this CI/CD setup makes your life easier. It's especially good for beginners and solo developers looking to automate deployments without self-hosting Jenkins or configuring GitHub Actions from scratch.

```
CodeCommit / GitHub → CodePipeline → CodeBuild → CodeDeploy → EC2 / ECS / Lambda
```
