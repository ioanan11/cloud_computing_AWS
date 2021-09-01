**How to configure a VM in AWS**

-after entering credentials to login, make sure location is set to Europe - Ireland

-in EC2 from menu, create an instance from "Launch Instance"

-choose an Amazon Machine Image (e.g. Ubuntu Server 16.04 LTS (HVM), SSD Volume Type)

-select t2.micro for instance type unless stated otherwise

-instance details: 
	number of instances: 1 (unless stated otherwise)
	network: vpc-07e(default)
	subnet: 0429...Student
	auto-assign public ip: enable

-next add storage (leave settings as they are unless stated otherwise)

-next add tags
	Key: Name
	Value: sre_ioana_app (keep the same name)

-next configure security group 
	select existing security group
	security group name: sre_ioana_app
	description: sre_ioana_app (type ssh, port 22)
	later other ports can be added (e.g. port 3000, custom TCP)

-to launch >> chmod 400 "the_key.pem"
   	   >> ssh -i "the_key.pem" "ip_address" (ip address is shown in instance summary on AWS): ssh -i "sre_key.pem" ubuntu@ec2-54-217-49-97.eu-west-1.compute.amazonaws.com

-voilla you have a VM running yay!

**How to copy a folder from local host in AWS VM**

-make sure all dependencies are installed!!!
	>>sudo apt-get update -y
	>>sudo apt-get upgrade -y
	>>sudo apt-get install nginx -y
	>>sudo apt-get install python-software-properties -y
	>>sudo apt-get install nodejs (if not installed properly use sudo apt install nodejs-legacy)

-use scp -ri ~/.ssh/sre_key.pem app ubuntu@<<ip_address>>:/home/ubuntu/app to copy folder app from local host (absolute path) to VM

-install and run npm
	>>node seeds/seed.js
	>>sudo npm install
	>>sudo npm start

-app should run on your ip address with port 3000. 
 