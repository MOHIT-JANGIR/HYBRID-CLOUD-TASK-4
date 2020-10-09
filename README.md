In this article we are going to discuss how to create vpc , subnet , Internet gateway, Nat gateway, routing table and launch Wordpress and MySQL instances on the top of public cloud aws using Terraform.

Pre-Requisites
We require AWS IAM API keys (access key and secret key) for creating and deleting permissions for AWS resources. 
Terraform should be installed on the Local VM.
Amazon Resources Created Using Terraform
Performing the following steps:

1. Write an Infrastructure as code using terraform, which automatically create a VPC.

2. In that VPC we have to create 2 subnets:

  1.  public subnet [ Accessible for Public World! ] 

  2.  private subnet [ Restricted for Public World! ]

3. Create a public facing internet gateway for connect our VPC/Network to the internet world and attach this gateway to our VPC.

4. Create a routing table for Internet gateway so that instance can connect to outside world, update and associate it with public subnet.

5. Create a NAT gateway for connect our VPC/Network to the internet world and attach this gateway to our VPC in the public network

6. Update the routing table of the private subnet, so that to access the internet it uses the nat gateway created in the public subnet

7. Launch an ec2 instance which has Wordpress setup already having the security group allowing port 80 sothat our client can connect to our wordpress site. Also attach the key to instance for further login into it.

8. Launch an ec2 instance which has MYSQL setup already with security group allowing port 3306 in private subnet so that our wordpress vm can connect with the same. Also attach the key with the same.



Note: Wordpress instance has to be part of public subnet so that our client can connect our site. 

mysql instance has to be part of private subnet so that outside world can't connect to it.

Don't forgot to add auto ip assign and auto dns name assignment option to be enabled.

AWS VPC
Amazon Virtual Private Cloud (Amazon VPC) lets you provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define. You can use both IPv4 and IPv6 in your VPC for secure and easy access to resources and applications.

_______________________________________________________
Start Building
I have created a folder name as tera and a file to write all the Terraform in this file name as project4.tf .

No alt text provided for this image
Step-1 - create vpc
First we need to create provider . The Amazon Web Services (AWS) provider is used to interact with the many resources supported by AWS. The provider needs to be configured with the proper credentials before it can be used.

Below Terraform code is to create aws VPC in which

cidr_block - is, When we create a VPC, you must specify a range of IPv4 addresses for the VPC in the form of a Classless Inter-Domain Routing (CIDR) block; for example, 10.0. 0.0/16.

No alt text provided for this image
Step-2-a - create public subnet
A public subnet is a subnet that's associated with a route table that has a route to an Internet gateway. A private subnet with a size /24 IPv4 CIDR block for example "192.168.0.0/24".

No alt text provided for this image
Step-2-a - create private subnet
No alt text provided for this image
now both the subnet are private, to make public one of the above subnet we need to create route table and Internet gateway for vpc and then associate to public subnet.

Step-3 - create Internet gateway
An internet gateway serves two purposes: to provide a target in your VPC route tables for internet-routable traffic, and to perform network address translation (NAT) for instances that have been assigned public IPv4 addresses.

No alt text provided for this image
Step-4 - create Routing table
A route table contains a set of rules, called routes, that are used to determine where network traffic from your subnet or gateway is directed.

After creating route table associate it with the one of the subnet to make it public.

No alt text provided for this image
Step-5 - create Nat gateway
NAT Gateway is a highly available AWS managed service that makes it easy to connect to the Internet from instances within a private subnet in an Amazon Virtual Private Cloud (Amazon VPC). Previously, you needed to launch a NAT instance to enable NAT for instances in a private subnet.

No alt text provided for this image
Step-6 - create Routing table
No alt text provided for this image
Step-7 - create security group and launch Wordpress instances
Below code is to create security group for wordpress.

A security group acts as a virtual firewall for your EC2 instances to control incoming and outgoing traffic.

No alt text provided for this image
Below code is to launch Worpress EC2 instances.

No alt text provided for this image
Step-8 - create security group and launch MySQL instances
Below code is to create security group for MySQL.

No alt text provided for this image
Below code is to launch MySQL database EC2 instances.

No alt text provided for this image
now initalise the tera tera directory using command.

Terraform init

No alt text provided for this image
to run the code terraform apply -auto-approve

No alt text provided for this image
No alt text provided for this image
and good practise to see everything is configured as it is or not . on aws console we can check.

vpc

No alt text provided for this image
Private subnet

No alt text provided for this image
Public subnet

No alt text provided for this image
Internet Gateway

No alt text provided for this image
Routing table

No alt text provided for this image
No alt text provided for this image
Nat gateway

No alt text provided for this image
No alt text provided for this image
Routing table

No alt text provided for this image
No alt text provided for this image
security group

No alt text provided for this image
Instance

No alt text provided for this image
now access the worpress using worpress public ip .

No alt text provided for this image
and to connect Worpress with MySQL database we need instance id of MySQL .

No alt text provided for this image
No alt text provided for this image
This is the final web page of wordpress .

No alt text provided for this image
