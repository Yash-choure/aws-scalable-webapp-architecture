# 🚀 Deploying a Java Web Application on AWS

This repository is a **case study and walkthrough** of how I designed and deployed a **scalable, production-ready cloud infrastructure** for a Java web application using **Amazon Web Services (AWS)**.  

⚠️ **Note**: The live application has been taken offline to reduce cloud costs. However, this repo remains as a detailed breakdown of the architecture, setup, and lessons learned.

---

## 🏛️ Cloud Architecture

To ensure **speed, scalability, security, and reliability**, I designed the following AWS architecture:

![AWS Architecture Diagram](./architecture-diagram.png) <!-- You can add your diagram file here -->

---

### 🌍 A User’s Journey Through the System

1. **Starting Point – Route 53 & CloudFront**  
   - User requests first hit **Route 53** (DNS).  
   - Requests are routed via **CloudFront (CDN)**, which caches static assets (images, CSS, JS) globally for faster load times.  

2. **Brains of the Operation – Elastic Beanstalk**  
   - For dynamic content, CloudFront forwards requests to an **Application Load Balancer (ALB)**.  
   - The ALB distributes traffic across EC2 instances managed by **Elastic Beanstalk**.  
   - Elastic Beanstalk automatically handles **Auto Scaling** and **load balancing**.  

3. **Secure Backend Components**  
   - **Amazon RDS**: Managed relational database (secure, patched, backed up).  
   - **Amazon ElastiCache (Redis)**: Caching frequently accessed data for performance.  
   - **Amazon MQ (RabbitMQ)**: Decoupling long-running tasks with message queues.  
   - All backend services placed inside a **private subnet & Security Group** (not exposed to the public).  

4. **Monitoring & Logging**  
   - **CloudWatch**: Metrics, alerts, and centralized monitoring.  
   - **Amazon S3**: Storing logs, artifacts, and static files.  

---

## 🛠️ Deployment Workflow

I took on the role of a **Cloud Engineer** and executed the deployment in these stages:

1. **Package the App**  
   - Cloned the existing source code  
   - Built using Maven:  
     ```
     mvn clean package
     ```  
   - Generated a `.war` file ready for deployment.  

2. **Build the Infrastructure**  
   - Set up **VPC, subnets, routing tables, internet/NAT gateways**  
   - Configured **security groups**  
   - Launched **RDS (DB)** and **Elastic Beanstalk (with Tomcat application server)**  

3. **Deploy to Elastic Beanstalk**  
   - Uploaded the `.war` package.  
   - Elastic Beanstalk rolled out the app across EC2 instances automatically.  

4. **Domain & Testing**  
   - Configured **Route 53** to point the domain to **CloudFront**, which directed traffic to the ALB & Beanstalk app.  
   - Performed end-to-end tests before going live.  

---

## 💡 Key Learnings

- **Cloud Architecture** – Designed a complete, production-level system from scratch.  
- **AWS Hands-On** – Gained practical experience with VPC, Elastic Beanstalk, RDS, CloudFront, Route 53, and more.  
- **DevOps Mindset** – Managed the full cycle: build → deploy → scale → monitor.  
- **Security Best Practices** – Segmented the infrastructure with private subnets, IAM/security groups, and restricted access.  

---

## 🧰 Tech Stack

- ☁️ **Cloud Provider**: AWS  
- ⚙️ **Deployment**: Elastic Beanstalk  
- 🔥 **Application Server**: Apache Tomcat  
- 🗄️ **Database**: Amazon RDS  
- ⚡ **Caching**: Amazon ElastiCache (Redis)  
- 📩 **Message Broker**: Amazon MQ (RabbitMQ)  
- 🛠️ **Build Tool**: Apache Maven  
- 💻 **Language / Stack**: Java  

---

## 📂 Project Repository

Original application code:  
👉 [Source Code Repository](https://github.com/hkhcoder/vprofile-project.git)  

---

## 👤 Author

**Your Name**  
💼 Cloud / DevOps Engineer  

---

✨ *This project was a hands-on journey into deploying scalable Java web applications in the AWS cloud — a real-world architecture designed for performance, security, and growth.*  

