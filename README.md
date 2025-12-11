🏗️ Project Overview

This project demonstrates a secure, production-style network pattern used by real companies:

A public bastion host (EC2) acts as the controlled entry point.

A private EC2 web server hosts an application without any public exposure.

The entire design enforces least privilege, segmented networks, and zero-trust access paths.

I built this architecture to showcase practical cloud engineering skills:
Networking, routing, SSH key management, IAM-less access, service hardening, and secure connectivity across tiers.

This project represents the level of hands-on infrastructure work I’ll be doing professionally as a Cloud/DevOps Engineer.

🔐 Why This Architecture Matters in the Real World

Companies do not expose internal services directly to the internet — they route access through tightly secured entry points.

This prevents:

External attack surface exposure

Lateral movement

Unrestricted SSH access

Accidental public DNS leaks

Bot scanning & brute-force attempts

A bastion → private server model is foundational to security-driven cloud deployments.

🧩 Architecture Diagram
                Internet
     (SSH allowed from my IP)
                     |
        Bastion Host (Public)
       EC2 – Amazon Linux 2023
                     |
         (Private VPC Routing)
                     |
      Private Web Server (EC2)
     Accessible only via Bastion Host

⚙️ Key Technical Components
1. VPC + Subnets

Public subnet for the bastion

Private subnet for the web server

Route tables configured so private subnet has no IGW access

2. Security Groups

Bastion SG: SSH allowed only from my IP

Private Web SG: SSH allowed only from Bastion SG, port 80 allowed internally

3. Bastion Host

Acts as a controlled “jump box”

Stores SSH key for private instance (with least privilege permissions)

No application workload runs here

4. Private Web Server

No public IP address

Accessible only through Bastion host

Hosts Apache (httpd) web service

5. User Data / Configuration

Apache installed and configured via:

sudo yum update -y
sudo yum install -y httpd
sudo systemctl enable httpd
sudo systemctl start httpd

🧪 Testing the Setup
From Bastion: Verify private connectivity
ssh -i ~/.ssh/my-keypair.pem ec2-user@10.0.2.220

After connecting: verify the web service
curl http://localhost


Successful output returns HTML from Apache.

🚀 How This Prepares Me For Cloud Engineer Roles

This project demonstrates:

✔️ Secure networking design

Segmentation, routing, NACL/Security Group enforcement.

✔️ Identity-less authentication (SSH key, not IAM)

Matches production SSH security patterns.

✔️ Building and troubleshooting EC2 connectivity

Bastion → private tier is a day-1 responsibility of Cloud/DevOps Engineers.

✔️ Linux administration

File permissions, services, logs, systemctl, yum, ownership, SSH key placement.

✔️ Production-style thinking

I had to reason about:

Least privilege

Attack surface reduction

Controlled ingress

Proper routing

Service uptime

This is exactly the type of engineering mindset companies look for.

📝 Interview-Ready Explanation

I built a secure two-tier architecture where a public bastion host is used to reach a private EC2 web server.
The private server has no public IP and can only be accessed through the bastion using SSH keys with strict file permissions.
I configured the networking, routing, and security groups to enforce least privilege, then installed Apache on the private host and validated connectivity from inside the VPC.
This project shows I can design secure cloud network patterns, troubleshoot connectivity, harden SSH access, and build production-style infrastructure — exactly what’s required for Cloud Engineer and DevOps roles.
