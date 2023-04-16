<h1>Deploy An EC2 Inside A Custom VPC</h1>
<!--
 ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo)
--!>
<h2>Description</h2>
A new startup business in North America has recruited you to help with the launch of a quick-access, low-cost static website. You've decided to complete this contract by hosting and deploying their website utilizing AWS S3
<br />

<h2>Solution Overview</h2>

- <b>Create your custom VPC
- Create VPC
- Create Subnet
- Create Internet Gateway
- Create Route Tables
- Create EC2 instance
- Create Security Group
- Deploy EC2 in public subnet
- Launch your website

<h2>Detailed Steps:</h2>

<p align="center">

View our Architecture

Navigate to VPC and select "Create VPC"

Give VPC a name tag: <br/> 
<img src="https://i.imgur.com/A3KD4lI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Click Create VPC

Navigate to Subnets on the left panel

Click Create Subnet
- We will be creating a public and a private subnet

Give the 1st Subnet (public subnet) a name tag

Select an availability zone

To calculate the CIDR range of your subnets, use this link: https://www.site24x7.com/tools/ipv4-subnetcalculator.html

To convert IP range to CIDR block, use this link https://www.ipaddressguide.com/cidr:  <br/>
<img src="https://i.imgur.com/hdT5cPI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/xLEIZj3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Give the 2nd Subnet (private subnet) a name tag
<img src="https://i.imgur.com/f6Ud3zL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
To give the public subnet access to the internet, we will to create an need an internet gateway
- Navigate to internet gateway on the left panel and select "Create Internet Gateway"


Give it a Name a tag and select "Create internet gateway" 

Now attach the internet gateway to your VPC by selecting your internet gateway, Actions and Attach to VPC
<img src="https://i.imgur.com/iO5JmhJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select your VPC and select "Attach internet gateway"

Now navigate to "Route table" and select "Create route table"
- This route table will allow resources to access the public internet by connecting to the internet gateway

Give it a name tag, select your VPC from the drop down menu, and then select "Create route table"

Select your created route table and navigate to "Subnet association" and select "Edit subnet association"
<img src="https://i.imgur.com/INbT3gs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Now select your public subnet and select "save association"
<img src="https://i.imgur.com/zFNe4dJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Now navigate to route and select "edit route" <br/>
<img src="https://i.imgur.com/J8N7rMz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Then create a route from destination 0.0.0.0/0 to target [your internet gateway]. Then save changes
<img src="https://i.imgur.com/eMOqoXi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now create navigate to your public subnet and select "Edit Route table association"
<img src="https://i.imgur.com/1G4BAnJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Under Route table ID, select your public route table and select "save"

Now create an EC2 instance that will be placed into the public subnet
- Navigate to EC2 and select "Launch instance"

Give it a name tag and Select Your AMI

Under "Instance Type" select t2.micro as this is free tier eligible
<img src="https://i.imgur.com/D3H3c3Z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Edit Network Settings and select your VPC (not the default VPC), public subnet (with the route to the internet gateway), enable Auto assign IP

For security group allow HTTP/HTTPS access from the public internet. Similar to below
<img src="https://i.imgur.com/ETq62WN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Under Advanced details, paste this under "User Data"
"#!/bin/bash
yum update -y
yum install httpd -y
echo "<html><h1>webpage 1(whatever you want, give the page name here)</h1></html>" > /var/www/html/index.html
service httpd start
chkconfig httpd on"
- Feel free to edit the user data


Now select “Launch Instance”.


Once the instance state is "Running", copy and paste the Public IP address to a web browser and you should see your website launch.
<img src="https://i.imgur.com/7td9JlW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>