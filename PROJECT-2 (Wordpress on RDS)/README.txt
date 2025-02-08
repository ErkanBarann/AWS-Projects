# AWS WordPress Auto Scaling & Load Balancer Setup

## **1. RDS and EC2 Setup**

To deploy **WordPress** on AWS, we set up an **RDS (MySQL Database)** and an **EC2 (Ubuntu Server)**. The **RDS was created first**, followed by the EC2 instance to ensure proper database connectivity.

### **1.1 Creating the RDS Database**
- Navigated to **Amazon RDS** in the AWS Console.
- Created a **MySQL database**.
- Configured the security group and allowed **port 3306** for EC2 access.

### **1.2 Setting Up the EC2 Ubuntu Server**
- **Launched an EC2 instance** using the Ubuntu AMI.
- **Connected to EC2 via SSH:**
  ```bash
  ssh -i key.pem ubuntu@your-ec2-public-ip
  ```
- **Installed Apache and PHP:**
  ```bash
  sudo apt update
  sudo apt install apache2 php libapache2-mod-php php-mysql -y
  ```
- If using **CentOS**, the Apache package is named `httpd`.

### **1.3 Testing EC2 and RDS Connection**
- **Verified MySQL connection from EC2 to RDS:**
  ```bash
  mysql -h <RDS_ENDPOINT> -u <DB_USER> -p
  ```
- Once the connection was successful, WordPress installation proceeded.

### **1.4 Installing and Configuring WordPress**
- **Downloaded and installed WordPress:**
  ```bash
  cd /var/www/html
  sudo wget https://wordpress.org/latest.tar.gz
  sudo tar -xvzf latest.tar.gz
  sudo mv wordpress/* .
  sudo chown -R www-data:www-data /var/www/html/
  sudo chmod -R 755 /var/www/html/
  ```
- **Updated wp-config.php:**
  ```php
  define('DB_NAME', '<DB_NAME>');
  define('DB_USER', '<DB_USER>');
  define('DB_PASSWORD', '<DB_PASSWORD>');
  define('DB_HOST', '<RDS_ENDPOINT>');
  ```
- **Restarted Apache:**
  ```bash
  sudo systemctl restart apache2
  ```

**At this stage, WordPress was accessible and fully operational.**

---

## **2. Auto Scaling and Load Balancer Configuration**

To enhance scalability, **Auto Scaling and a Load Balancer** were configured.

### **2.1 Creating AMI and Launch Template**
- **Created an AMI (Amazon Machine Image) from the existing EC2 instance.**
- **Created a Launch Template** using this AMI.

### **2.2 Setting Up Target Group and Load Balancer**
- **Created a Target Group.**
- **Added the existing EC2 instance to the Target Group.**
- **Allowed inbound access to port 80 in the security group.**
- **Created a Load Balancer.**
- **Configured Security Group rules to allow external traffic on port 80.**
- **Set up Health Check (path: `/index.php`).**
- **Granted SSH access for Load Balancer Security Group.**

### **2.3 Configuring Auto Scaling Group**
- **Created an Auto Scaling Group with:**
  - **Min:** 1
  - **Max:** 4 (Optionally 3)
  - **Desired Capacity:** 2
- **No Dynamic Scaling Policy was added.**
  - The system does not automatically add or remove instances based on CPU or RAM thresholds, running in a standard configuration.

### **2.4 Security Group Configuration**
#### **EC2 Security Group**
- **Inbound Rules:**
  - **SSH (22)** → Restricted to specific IP addresses.
  - **HTTP (80)** → Open to all (`0.0.0.0/0`, `::/0`).
  - **HTTPS (443)** → Open if SSL is required.
  - **MySQL/Aurora (3306)** → Restricted to EC2 instances needing database access.

#### **RDS Security Group**
- **Inbound Rules:**
  - **MySQL/Aurora (3306)** → Restricted **only** to the EC2 Security Group.

#### **Load Balancer Security Group**
- **Inbound Rules:**
  - **HTTP (80)** → Open to all (`0.0.0.0/0`, `::/0`).
  - **HTTPS (443)** → Open if SSL is enabled.
- **Outbound Rules:**
  - **Allow all outgoing traffic (`0.0.0.0/0`, `::/0`).**

### **2.5 Final Testing and Validation**
- **Verified that the system was running across two EC2 instances through the Load Balancer.**
- **Tested access via the Load Balancer DNS.**
- **Health Check confirmed that both instances were operational.**

---

## **3. Conclusion**
This project successfully deployed a **scalable WordPress environment on AWS**. **EC2 and RDS were configured, and the system was strengthened using Auto Scaling and a Load Balancer.**

For future improvements, **dynamic scaling policies** (based on CPU or memory thresholds) can be implemented in **AWS Auto Scaling** to optimize resource allocation.

📌 **This architecture follows AWS best practices, ensuring high availability and flexibility.** 🚀

