# 🛡️ VPC with Public-Private Subnets in Production

This project demonstrates how to create a **secure VPC architecture** for production with **auto scaling** and **application load balancing**.

---

## 1️⃣ Create VPC

Go to **VPC Dashboard → Create VPC**  
Choose **VPC and more**

- **Name**: MyVPC  
- **IPv6**: Disable  
- **Availability Zones**: 2  
- **Public Subnets**: 2 (one per AZ)  
- **NAT Gateways**: 1 per AZ  

✅ Enable:
- DNS Hostnames
- DNS Resolution

🚀 Automatically creates:
- Internet Gateway (attached to VPC)
- Route Tables (associated with subnets)
- Elastic IPs for NAT Gateways

👉 Click **Create VPC**

---

## 2️⃣ Create Auto Scaling Group

### a. Create Launch Template

Go to **EC2 Dashboard → Launch Templates → Create Launch Template**

- Select existing or create new **Key Pair**
- **Security Group**:  
  - Name: `PrivateEC2SG`  
  - Allow HTTP (8000) from within VPC  
  - Deny public access

### b. Create Auto Scaling Group

Go to **Auto Scaling Groups → Create Auto Scaling Group**

- Select the **launch template** created above
- **Network**: Select **private subnets** in both AZs
- **Group Size**:  
  - Desired: 2  
  - Minimum: 1  
  - Maximum: 4

👉 Click **Create**

---

## 3️⃣ Create Bastion Host (Jump Box)

Go to **EC2 Dashboard → Launch Instance**

- **Name**: BastionHost  
- **Subnet**: Public Subnet in AZ-a  
- **Security Group**:  
  - Allow SSH (TCP 22) **from your IP only**
- Use the same **Key Pair** used above  
- 👉 Launch Instance

---

## 4️⃣ Access Private EC2 via Bastion Host

1. **Copy key pair to Bastion Host**
   ```bash
   scp -i your-key.pem your-key.pem ec2-user@<Bastion-IP>:~/
   ```

2. **SSH into Bastion Host**
   ```bash
   ssh -i your-key.pem ec2-user@<Bastion-IP>
   ```

3. **SSH into Private EC2 from Bastion**
   ```bash
   ssh -i your-key.pem ec2-user@<Private-EC2-IP>
   ```

4. **Start the application on port 8000**
   ```bash
   python3 your_app.py
   ```

---

## 5️⃣ Create Application Load Balancer

Go to **Load Balancers → Create Load Balancer**

- **Type**: Application Load Balancer  
- **Name**: MyALB  
- **Scheme**: Internet-facing  
- **Listeners**: HTTP (80)  
- **AZs/Subnets**: Select **public subnets**

### a. Create Target Group

Go to **Target Groups → Create Target Group**

- **Name**: `PrivateEC2TG`  
- **Protocol**: HTTP  
- **Port**: 8000  
- **Target Type**: Instance  
- **Register** private EC2 instances  
- 👉 Click **Create**

### b. Attach Target Group to ALB

- During ALB setup, select `PrivateEC2TG` as the **target group**  
- 👉 Click **Create Load Balancer**

---

## 6️⃣ Access the Application

1. Go to **EC2 → Load Balancers**
2. Copy the **DNS name** of the ALB
3. Paste it in your browser  
✅ You should see the application running on **port 8000**

---

## ✅ Summary

- Secure application inside **private subnet**
- **Bastion Host** to access private EC2
- **NAT Gateway** for internet access from private EC2s
- **Auto Scaling** for resilience
- **ALB** for load balancing traffic to your application