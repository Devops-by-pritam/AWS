# AWS EC2 & Security Concepts

## 🔐 Security Group (Instance Level Firewall)
- **Acts at the EC2 instance level** (i.e., attached to network interfaces).
- **Stateless vs Stateful:**
  - Security Groups are **stateful** – if you allow inbound traffic, the response is automatically allowed.
- **Inbound Rules** (Traffic coming *into* your EC2 instance):
  - By default, **all inbound traffic is denied**.
  - You need to manually **allow ports** like:
    - Port 22 (SSH) – for Linux instance access.
    - Port 3389 (RDP) – for Windows instance.
    - Port 8000 (your Python app).
    - Port 80 (HTTP) or 443 (HTTPS) for web servers.
- **Outbound Rules** (Traffic going *out* from your EC2 instance):
  - By default, **all outbound traffic is allowed**.
  - You can restrict this if needed (e.g., allow only specific IPs, ports, or protocols).

---

## 🌐 NACL (Network Access Control List)
- Acts at the **subnet level**, not at instance level.
- **Stateless** – you must define **both inbound and outbound** rules explicitly.
- Rules are processed in **order** (lowest rule number first).
- Useful to **allow or deny** traffic at a broader level (e.g., entire subnet).
- Supports **"DENY" rules**, unlike Security Groups (which only allow).

---

## 💻 EC2 Instance Creation Steps

1. **Choose an Amazon Machine Image (AMI)**
   - e.g., Ubuntu, Amazon Linux, Windows, etc.

2. **Select Instance Type**
   - e.g., t2.micro (Free Tier eligible)

3. **Configure Instance**
   - Set number of instances, IAM role, shutdown behavior, etc.

4. **Configure Network**
   - Select the **VPC** (Virtual Private Cloud) created earlier.
   - Choose a **Subnet** (if you have multiple).
   - **Enable Auto-Assign Public IP** if you want internet access.

5. **Add Storage**
   - Configure root volume or add additional EBS volumes.

6. **Add Tags**
   - Useful for cost tracking and organization (e.g., Name: WebServer).

7. **Configure Security Group**
   - Create a new one or choose an existing group.
   - Allow required ports (22, 80, 443, 8000, etc.).

8. **Review and Launch**
   - Review all configurations.
   - Choose/create a key pair for SSH access.

---

## ⚙️ After Launch – Instance Configuration

1. **SSH into the Instance**
   ```bash
   ssh -i your-key.pem ec2-user@your-public-ip
   ```

2. **Install Python and Application Dependencies**
   ```bash
   sudo apt update
   sudo apt install python3 python3-pip -y
   ```

3. **Run Your Python Application (on port 8000)**
   ```bash
   python3 your_app.py
   ```

4. **Make Sure Security Group Allows Port 8000**
   - Add a custom TCP rule:
     - **Type**: Custom TCP
     - **Port Range**: 8000
     - **Source**: 0.0.0.0/0 (for public access)

---

## 📝 Tips

- Always **restrict access** to your application and ports using CIDR blocks (`<IP>/32` for single IP).
- Use **Elastic IP** if your public IP should not change after instance reboot.
- Use **User Data** to automate app installation on launch.
- Monitor traffic using **VPC Flow Logs** or **CloudWatch**.
