# AWS WordPress Auto Scaling, Load Balancer & RDS Setup

## 1. Creating Security Groups

Before deployment, it is necessary to configure the required **Security Groups** for **EC2, RDS, Load Balancer, and Target Group**. This ensures seamless communication between system components in later stages.

### 1.1 EC2 Security Group

- **SSH (22):** 🔒 Used for secure connections. Initially, it is left open to all (`0.0.0.0/0`, `::/0`) for easy access. However, for security reasons, it is recommended to restrict access to specific IP addresses.
- **HTTP (80) and HTTPS (443):** 🌐 Initially opened to allow external access (`0.0.0.0/0`, `::/0`).

👜 **Important Note:** When adding EC2 to the **Load Balancer**, modify **HTTP (80) and HTTPS (443) rules** to ensure traffic is only directed through the Load Balancer. To prevent direct access, restrict **EC2 Security Group HTTP/HTTPS traffic to requests coming only from the Load Balancer Security Group.**

### 1.2 RDS Security Group

- **MySQL/Aurora (3306):** ✅ Allowed only for the related EC2 Security Group.

### 1.3 Load Balancer Security Group

- **HTTP (80):** 🌎 Open to all (`0.0.0.0/0`, `::/0`).
- **HTTPS (443):** 🔐 Open if SSL is required.
- **Outbound:** 🚀 All traffic is allowed (`0.0.0.0/0`, `::/0`).

### 1.4 Target Group Security Group

- **HTTP (80):** 📡 Allowed only for traffic from the Load Balancer.
- **Outbound:** 🔄 Allowed for traffic routed to EC2 instances.

---

## 2. RDS and EC2 Setup

To deploy **WordPress** on AWS, an **RDS (MySQL Database)** and an **EC2 (Ubuntu Server)** were set up. **The RDS was created first**, followed by the EC2 instance to establish the database connection.

### 2.1 Creating the RDS Database

- 🔹 Logged into **Amazon RDS** service.
- 🛠 Created a **MySQL database**.
- 🔒 Added the previously created **RDS Security Group**.

### 2.2 Setting Up the EC2 Ubuntu Server

- 🖥 **Launched an EC2 instance** using the Ubuntu AMI.
- 🔑 **Selected the previously created EC2 Security Group.**
- 📡 **Connected to EC2 via SSH:**
  ```bash
  ssh -i key.pem ubuntu@your-ec2-public-ip
  ```
- ⚙ **Installed Apache and PHP:**
  ```bash
  sudo apt update
  sudo apt install apache2 php libapache2-mod-php php-mysql -y
  ```

### 2.3 Testing EC2 and RDS Connection

- ✅ **Verified MySQL connection from EC2 to RDS:**
  ```bash
  mysql -h <RDS_ENDPOINT> -u <DB_USER> -p
  ```
- 🛠 Once the connection was successful, WordPress installation proceeded.

### 2.4 Installing and Configuring WordPress

- 👅 **Downloaded and installed WordPress:**
  ```bash
  cd /var/www/html
  sudo wget https://wordpress.org/latest.tar.gz
  sudo tar -xvzf latest.tar.gz
  sudo mv wordpress/* .
  sudo chown -R www-data:www-data /var/www/html/
  sudo chmod -R 755 /var/www/html/
  ```
- ⚙ **Updated wp-config.php:**
  ```php
  define('DB_NAME', '<DB_NAME>');
  define('DB_USER', '<DB_USER>');
  define('DB_PASSWORD', '<DB_PASSWORD>');
  define('DB_HOST', '<RDS_ENDPOINT>');
  ```
- 🔄 **Restarted Apache:**
  ```bash
  sudo systemctl restart apache2
  ```

🚀 At this stage, **WordPress was accessible and fully operational.**

---

## 3. Auto Scaling and Load Balancer Configuration

### 3.1 Target Group and Load Balancer Configuration
📌 **The Target Group should be created first**, followed by linking the Load Balancer to this Target Group. This is because the Load Balancer requires a target group during setup.

- ⚙ **Created a Target Group and configured it to listen on HTTP port 80.**
- ✅ **Added the existing EC2 instance to the Target Group.**
- 🏰 **Then created a Load Balancer and linked it to the Target Group.**
- 🔒 **Updated the EC2 security group so that HTTP/HTTPS traffic is now limited to requests from the Load Balancer.**

### 3.2 Auto Scaling Group Configuration

- 🏰 **Created an AMI (Amazon Machine Image) from the existing EC2 instance.**
- 🛠 **Created a Launch Template using this AMI.**
- 🚀 **Set up an Auto Scaling Group using the Launch Template.**
- 👕 **Minimum:** 1, **Maximum:** 4, **Desired Capacity:** 2.
- 📈 **Dynamic scaling (CPU, memory, and network-based scaling) can be optionally added.**

---

## 4. Conclusion

This project successfully deployed a **scalable WordPress environment on AWS.**

### **AWS Services Used in This Project:**
- ☁ **Amazon EC2:** For hosting the WordPress web server.
- 📄 **Amazon RDS:** For managing and storing the MySQL database.
- 📦 **Amazon S3 (Optional):** Can be used for centralized storage of WordPress media files.
- ⚖ **Elastic Load Balancer (ELB):** To distribute incoming HTTP traffic to EC2 instances.
- 🔄 **Auto Scaling Group:** To add new EC2 instances when traffic increases and maintain balance.
- 📊 **Amazon CloudWatch (Optional):** Can be used for monitoring server performance and enabling dynamic scaling.

👜 **This architecture follows AWS best practices, ensuring high availability, scalability, and reliability for a robust WordPress deployment.** 🚀

