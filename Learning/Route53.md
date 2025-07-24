# 🌐 AWS Route 53 & DNS Basics

## 📘 What is Route 53?
- **Route 53** is Amazon Web Services' **DNS (Domain Name System) web service**.
- It is highly **available**, **scalable**, and **reliable**.
- Provides services like:
  - **Domain registration**
  - **DNS routing**
  - **Health checking**

---

## ❓ What is DNS?

### DNS = Domain Name System
- DNS is like the **phonebook of the internet**.
- It maps **domain names (like `example.com`)** to **IP addresses (like `192.0.2.1`)**.
- Without DNS, you'd need to remember IPs instead of domain names to access websites.

---

## 🔁 What Does DNS Do?

- Translates **human-readable domain names** to **machine-understandable IP addresses**.
- Maintains various **DNS record types**:
  - **A record** – maps domain to IPv4 address
  - **AAAA record** – maps domain to IPv6 address
  - **CNAME** – alias for another domain
  - **MX** – mail exchange record
  - **NS** – nameserver records
  - **TXT** – text information (e.g., SPF, DKIM)

---

## 🌍 Domain Registration Options

1. **Buy Domain via AWS Route 53**
   - Simplified integration with AWS services.
   - Managed through the AWS Management Console.
   - Comes with default hosted zone setup.

2. **Host Domain Using Route 53 (External Registrar)**
   - Buy domain from providers like GoDaddy, Namecheap, etc.
   - Update the domain’s **nameservers** to AWS Route 53 NS records.
   - Create a **Hosted Zone** in Route 53 to manage DNS records for the domain.

---

## ✅ Summary

- Route 53 is AWS's **managed DNS and domain registration** service.
- DNS translates **domain names to IPs**.
- You can **buy and manage domains** directly in AWS or **migrate** your existing domain to be managed via Route 53.
