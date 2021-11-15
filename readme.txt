Cloudformation Exercise

Three files are included:

 1. kg-vpc.json
    kg-vpc.yml, for documentation purposes

2.  kg-alb-ec2.json
    kg-alb-ec2.yml, for documentation purposes

3.  kg-sqs.json
    kg-sqs.yml, for documentation purposes


1. kg-vpc.json , creates the following:

	1. Create VPC
	2. Create Internet Gateway
	3. Attach the Internet Gateway to the VPC
	4. Create the Public Subnets
	5. Create Public Route Table
	6. Add Public Route to the Public Route Table
	7. Associate the Public Subnets with the Public Route Table
	8. Create the Security Groups
	9. Export VPC ID
	10. Export Public Subnet 1
	11. Export Public Subnet 2
	12. Export ALB Security group
	13. Export EC2 Security group

2.  kg-alb-ec2.json, creates the following:

	1. Create Application Load Balancer
	2. Create Listener on port 80
	3. Create a Target Group and attach an existing EC2 instance
	4. Create an EC2 instance
	     1. aws cli is installed when EC2 is created
	     2.EC2 Instance ID is printed on the console
	5. Create an Instance profile for EC2 instance
	6. Create a Service Role for EC2 instance
	     1. This role is required for being able to run aws sqs ... command
	7. Cerate Policy for the role for EC2 instance
	8. Export for ALB DNS name

3. kg-sqs.json

	1. Create SQS
	2. aws sqs get-queue-url --region eu-west-1 --queue-name  kg-queue, region must be specified before running the command, within EC2 instance	


Key points:


EC2 instance is launched in the public subnet, to avoid creating a NAT Gateway and Jump box, which otherwise would be needed should EC2 instance was launched in private subnet.

Nonetheless, should a web server, i.e. be launched in EC2 instance, still, it wouldn’t be possible to access it directly, because ALB security group is an input to the EC2 security group.

Port 22 is allowed to be accessed from 0.0.0.0/0, for managing/testing an EC2 instance.

I have made no use of Parameters in the templates, by hardcoding the values, considering the nature of exercise.

AMI image ID is hardcoded to, and is a value from eu-west-1 region (Ireland) where all the templates should be run. If there is a specific reason to run it in another region then AMI image ID should be changed appropriately.

If kg-alb-ec2.json template, is to be run again from scratch, the name of the Role in the template should be changed to a name of the Role that doesn’t exist. In fact, before you run this template, the name of the Role chosen in the template, should not exist.

It is expected that key pair for EC2 is created in eu-west-1 region (Ireland), you will be prompted to make use of it, for purposes of accessing EC2 instance.


Scripting Exercise

I have used Node JS to complete this exercise
I have used two modules
    1. Axios, used for get request to the URL specified
    2. Readline, used  for command line input
Program is short, explanation provided in the code itself

	