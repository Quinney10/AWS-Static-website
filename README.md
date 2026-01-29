 **Free-Tier Static Website on AWS Using Terraform**  

For this project, I built a public static website hosted on AWS using Terraform as Infrastructure as Code (IaC). The goal of the project was to gain hands-on experience with core AWS services while ensuring the solution remained 100% within AWS Free Tier limits.

The services used in this project are:
-	Amazon EC2
-	Amazon VPC
-	Subnets
-	Internet Gateway
-	Security Groups

----------------------

**Project Setup**

I began by creating a new project directory named AWS-Static-Website. Inside this directory, I created the following Terraform files:
-	main.tf – Defines all AWS infrastructure resources
-	variables.tf – Stores configurable values such as region and SSH access IP
-	outputs.tf – Outputs useful information after deployment
-	README.md – Documents the project setup and usage

The outputs file was created so that once Terraform finishes deploying the infrastructure, the website URL is automatically displayed, making it easy to access the deployed site.
The variables file allows values such as the AWS region and SSH access IP to be easily modified without changing the core infrastructure code. This improves flexibility and follows Terraform best practices.

----------------------

**Infrastructure Overview**

All infrastructure is defined in main.tf, where I provisioned:
-	A custom VPC
-	A public subnet
-	An Internet Gateway
-	Route tables for internet access
-	A security group
-	An EC2 instance running a static website

The EC2 instance runs a web server configured through a user data script, allowing the website to be automatically deployed when the instance is launched.

----------------------

**Security Considerations**

To secure the environment, I restricted SSH access to the EC2 instance by allowing only my public IP address to connect over port 22. This was implemented using an AWS security group, ensuring that SSH access is not exposed to the public internet.

----------------------
**Errors Encountered and Resolving Them**

While running terraform plan, I encountered the following error:

Error: "" isnota validCIDRblock: invalid CIDRaddress withaws_security_group.web_sg, onmain.tf line39

This error occurred because the my_ip variable had been declared but not assigned a value. Terraform attempted to use an empty string as a CIDR block, which is invalid.

Solution
To resolve this issue, I created a terraform.tfvars file and defined the required variables:

- my_ip = "00.000.000.00/32" 
- key_name = "projects-key-pair" 

By using a terraform.tfvars file, sensitive information such as my public IP address and key pair name is kept out of the main Terraform files. This also ensures that sensitive data is not committed to GitHub, following security best practices.

----------------------

Created By Adam Q
