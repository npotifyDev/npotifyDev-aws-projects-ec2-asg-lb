#ec2-asg-lb
Project Description

This project demonstrates how to deploy a scalable web application on AWS using EC2, Auto Scaling Group (ASG), and an Application Load Balancer (ALB).
The web application is a simple Apache server that displays a custom message with the instance hostname.

- Skills demonstrated:

- Creating and configuring EC2 instances

- Creating AMIs for automated instance replication

- Configuring ALB with target groups for load balancing

- Setting up Auto Scaling for high availability and fault tolerance

- Implementing scaling policies based on CPU usage

- Writing reusable shell scripts for web server setup


Steps to Reproduce

Launch EC2 Instance

Amazon Linux 2, t2.micro

Run scripts/setup-webserver.sh to install Apache and create a sample webpage

sudo yum update -y
sudo yum install -y httpd
echo "Hello from $(hostname)" > /var/www/html/index.html
sudo systemctl enable httpd
sudo systemctl start httpd


Create AMI

From the EC2 instance → create an AMI for ASG

Create Application Load Balancer (ALB)

Navigate to EC2 → Load Balancer → Create ALB

Select public subnets and security groups allowing HTTP (80)

Create a Target Group and register your EC2 instance

Configure Auto Scaling Group (ASG)

Go to EC2 → Auto Scaling Groups → Create ASG

Launch template: use AMI created earlier

Instance type: t2.micro

Group size: Desired = 2, Min = 1, Max = 3

Attach ASG to the Target Group of ALB

Add scaling policies:

Scale out: CPU > 60%

Scale in: CPU < 20%

Test Scaling

Stop an EC2 instance → ASG should launch a new one

Visit ALB DNS → should display “Hello from …” from any instance