# Ansible & Terraform Lab - Week 11

## Overview
This project demonstrates the use of **Terraform** for provisioning AWS infrastructure and **Ansible** for configuring the instances. The final result is an Nginx server on Ubuntu displaying a web page and a Redis server on Rocky Linux.

---

## Steps taken

### **Step 1: Clone the Starter Code Repository**
```bash
git clone https://gitlab.com/cit_4640/4640-w11-lab-start-w25.git
cd 4640-w11-lab-start-w25
```

### **Step 2: Create an AWS SSH Key**
1. Generate a new SSH key:
```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/aws
```
2. Import the newly created key into AWS using the provided script:
```bash
./scripts/import_lab_key
```

### **Step 3: Deploy the Infrastructure Using Terraform**
1. Initialize Terraform:
```bash
terraform init
```
2. Apply the Terraform configuration to create the EC2 instances:
```bash
terraform apply
```

### **Step 4: Verify the Instances**
- Confirm the instances are running in the AWS Console.
- Check the SSH connectivity to the instances:
```bash
ssh -i ~/.ssh/aws ubuntu@<Ubuntu-Server-Public-IP>
ssh -i ~/.ssh/aws rocky@<Rocky-Server-Public-IP>
```

### **Step 5: Set Up Ansible Configuration**
1. Navigate to the Ansible directory:
```bash
cd ansible
```
2. Install the required Ansible dependencies (if missing):
```bash
ansible-galaxy collection install amazon.aws
```
3. Confirm inventory file is correctly configured by running:
```bash
ansible-inventory -i inventory/aws_ec2.yml --list
```

### **Step 6: Refactor `play.yml` to `playbook.yml` and Break into Roles**
1. Refactored the Ansible configuration to:
   - Include roles for **Redis** and **Nginx**.
   - Added handlers for Nginx reload when configuration changes.
2. Moved appropriate files into:
   - `roles/frontend_server/files/` (for `default.conf`).
   - `roles/frontend_server/templates/` (for `index.html.j2`).

### **Step 7: Run Ansible Playbook**
```bash
ansible-playbook -i inventory/aws_ec2.yml playbook.yml
```

### **Step 8: Verify Nginx Web Page**
- Open the following link in your browser to confirm the web page is served correctly:  
**[http://44.246.118.36/](http://44.246.118.36/)**

### **Step 9: Capture the Victory Screenshot**
Captured the screenshot of the successfully served webpage (shown below).

---

## **Victory Screenshot**
![Screenshot 2025-03-21 151151](https://github.com/user-attachments/assets/138de95d-61a1-4dc9-ad63-f7f310505936)



