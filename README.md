

My Project: Deploying a Java Web App on AWS
This project is a breakdown of how I designed and deployed a scalable, real-world cloud infrastructure for a Java web application. The main goal wasn't to write the app's code, but to build the robust cloud environment it runs on.

A quick heads-up: I've since taken the live application offline to manage cloud costs, but this repository serves as a detailed case study of the architecture and my process.

🏛️ The Cloud Architecture I Designed
To make sure the application was fast, reliable, and could handle plenty of users, I designed the following architecture on AWS. The diagram shows how a visitor's request flows through the entire system from start to finish.

A User's Journey Through the System:
Here’s a step-by-step look at how it all works together:

Starting Point (Route 53 & CloudFront): When you visit the site, your request first hits Route 53, which is AWS's DNS service. From there, it's sent to Amazon CloudFront, a CDN that keeps copies of static content (like images and CSS) in servers all over the world. This means the site loads much faster for everyone.

The Brains of the Operation (Elastic Beanstalk): For the dynamic parts of the site, CloudFront passes the request to an Application Load Balancer. This balancer's job is to spread the traffic evenly across multiple EC2 instances (the actual servers). I used Elastic Beanstalk to manage these servers in an Auto Scaling Group, which is a cool feature that automatically adds or removes servers depending on how busy the site gets.

The Secure Backend: The servers talk to the backend services, which I kept in a private, secure zone (Backend-sg) that isn't accessible from the open internet.

To speed things up, I used ElastiCache as a super-fast in-memory cache. This prevented the app from having to constantly ask the database for the same information.

The main database was a managed RDS instance, which is great because AWS handles all the boring stuff like patches and backups.

I also set up Amazon MQ as a message queue. This let the web servers hand off long-running tasks to a background process, so the user never had to wait.

Keeping an Eye on Everything (CloudWatch & S3): I used CloudWatch to monitor the entire system. It collected logs and performance metrics, so I could see if anything was going wrong. I also used an S3 bucket to store all those logs and other static files.

📝 My Role and How I Deployed It
For this project, I took on the role of a Cloud Engineer. My job was to take the existing application code, design the entire cloud infrastructure from the ground up, and then deploy the app.

You can find the original application's source code here: [PASTE THE LINK to your lecturer's public GitHub repository here]

Here was my game plan:
Package the App: First, I cloned the source code and used Maven to package the application into a .war file, which is a format that's ready for deployment. The command for this was mvn clean package.

Build the Infrastructure: I then went into the AWS Console and, following my architecture diagram, manually set up all the different services—the networking (VPC, subnets), security groups, the RDS database, and the Elastic Beanstalk environment.

Deploy! With the infrastructure in place, I uploaded the .war file I'd made to Elastic Beanstalk. It took over from there, automatically pushing the application out to all the EC2 servers.

Final Checks: To finish, I pointed the domain to the CloudFront distribution using Route 53 and did a full round of testing to make sure every part of the system was working perfectly.

💡 What I Learned
This project was a fantastic learning experience and gave me some real-world practice in a few key areas:

Cloud Architecture: I got to design a complete, production-ready cloud system from scratch.

Hands-On with AWS: I moved beyond theory and got practical experience setting up and connecting a wide range of AWS services.

The DevOps Mindset: I learned what it takes to bridge the gap between code and a live application, managing the entire deployment pipeline.

Security in the Cloud: I saw firsthand how important it is to build a secure environment by properly configuring networks and permissions.

🛠️ The Tech I Used
Cloud Provider: AWS (Amazon Web Services)

Deployment Orchestration: AWS Elastic Beanstalk

Build Tool: Apache Maven

Application Stack: Java
