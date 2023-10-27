# HTML-website


Title: Host an HTML website on a single EC2 instance in the default VPC
Solution Steps
-	Created Security Group with inbound rules for SSH and HTTP
o	NB SSH rule gives “Failed to fetch” error message when “My IP” is selected for the Source. To resolve this issue, “Anywhere-IPv4” is selected initially to create the Security Group. After the EC2-Instance is launched with the created Security Group, the Security Group inbound rule for the SSH is edited with the Source changed to “My IPv4”
-	Create EC2 Keypair of type RSA and format .pem
-	Launch EC2-Instance using Amazon Linux 2 AMI with t2.micro Instance type, select the key pair name created earlier, choose default VPC, and select created Security Group 
-	On PowerShell terminal SSH connection was established using the command
o	ssh -i <path to the private key of the EC2 keypair created> <username of the host machine>@<public IP address>
e.g., ssh -i ./Downloads/DemoEC2KeyPair.pem ec2-user@54.196.10.79
-	Then below commands were run on the command terminal
o	yum update -y
o	yum install -y httpd
o	cd /
o	cd var
o	cd www
o	cd html
o	wget https://github.com/adeoyedewale/HTML-website/archive/refs/heads/main.zip
o	unzip main.zip
o	cd HTML-website-main/
o	unzip mole.zip
o	cd /var/www/html
o	cp -r HTML-website-main/mole-main/* /var/www/html
o	rm -rf *.md *.zip HTML-website-main
o	systemctl enable httpd
o	systemctl start httpd
-	NB When getting the link for the wget command, click on Code on the GitHub reo and right-click on the Download ZIP for the correct kink to down the zipped file.
From above list of commands, the script suitable for GitHub Hosting is below:
#!/bin/bash
sudo su
yum update -y
yum install -y httpd
cd /var/www/html
wget https://github.com/adeoyedewale/HTML-website/archive/refs/heads/main.zip
unzip main.zip
unzip HTML-website-main/mole.zip
cp -r mole-main/* /var/www/html
rm -rf *.zip *.md HTML-website-main mole-main
systemctl enable httpd
systemctl start httpd

 





#! /bin/bash
sudo su
yum update -y
yum install -y httpd
cd /var/www/html
wget https://github.com/adeoyedewale/HTML-website/archive/refs/heads/main.zip
unzip main.zip
unzip HTML-website-main/mole.zip
cp -r mole-main/* /var/www/html
rm -rf *.zip *.md HTML-website-main mole-main
systemctl enable httpd
systemctl start httpd


Task 2
Solution Steps
-	Created a Key Pair with the Private Key downloaded to local machine project directed
-	Create a Security Group with two inbound rules:
o	SSH with My IP selected for Source info
o	HTTP with Antwhere-IPv4 selected for Source Info
-	Create an IAM role with attached Permission Policy of AmazonS3ReadOnlyAccess
-	Launch an ec2-Instance with Amazon Linux 2 AMI with t2.micro Instance type, created Key Pair,  Default VPC, created Security Group, and created IAM role attached (To attach the IAM Instance Profile, check the Advanced details section).
-	Create an S3 bucket and upload mole.zip file to the bucket
-	Establish SSH connection between ec2 Instance and local machine on PowerShell terminal using the command:
o	ssh -i <path to the private key of the EC2 keypair created> ec2-user@<public IP address>
-	Input following commands manually
o	sudo su
o	yum update -y
o	yum install -y httpd
o	cd /var/www/html
o	aws s3 sync s3://eruobodo-web /var/www/html
o	unzip mole.zip
o	cp -r /var/www/html/mole-main/* /var/www/html
o	rm -rf mole.zip mole-main
o	systemctl enable httpd
o	systemctl start httpd
-	Paste ec2 Instance public IP to browser to test the website.
-	Create a bash script from the commands as shown below:
o	 
-	Launch a new EC2 Instance using the script in the user data of the Advanced details section.
