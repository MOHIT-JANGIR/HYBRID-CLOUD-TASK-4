# <p align="center">hybrid cloud task 4</p>
# In this article we are going to discuss how to create vpc , subnet , Internet gateway, Nat gateway, routing table and launch Wordpress and MySQL instances on the top of public cloud aws using Terraform.

# Pre-Requisites


## *We require AWS IAM API keys (access key and secret key) for creating and deleting permissions for AWS resources.*
## *Terraform should be installed on the Local VM.*
## *Amazon Resources Created Using Terraform*

# Performing the following steps:

## 1. Write an Infrastructure as code using terraform, which automatically create a VPC.

## 2. In that VPC we have to create 2 subnets:

###  1.  public subnet [ Accessible for Public World! ] 

###  2.  private subnet [ Restricted for Public World! ]

## 3. Create a public facing internet gateway for connect our VPC/Network to the internet world and attach this gateway to our VPC.

## 4. Create a routing table for Internet gateway so that instance can connect to outside world, update and associate it with public subnet.

## 5. Create a NAT gateway for connect our VPC/Network to the internet world and attach this gateway to our VPC in the public network

## 6. Update the routing table of the private subnet, so that to access the internet it uses the nat gateway created in the public subnet

## 7. Launch an ec2 instance which has Wordpress setup already having the security group allowing port 80 sothat our client can connect to our wordpress site. Also attach the key to instance for further login into it.

## 8. Launch an ec2 instance which has MYSQL setup already with security group allowing port 3306 in private subnet so that our wordpress vm can connect with the same. Also attach the key with the same.



# `Note: Wordpress instance has to be part of public subnet so that our client can connect our site. `

# `mysql instance has to be part of private subnet so that outside world can't connect to it.`

# `Don't forgot to add auto ip assign and auto dns name assignment option to be enabled.`

# AWS VPC
## Amazon Virtual Private Cloud (Amazon VPC) lets you provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define. You can use both IPv4 and IPv6 in your VPC for secure and easy access to resources and applications.

_____________________________________________________________________________________________________________________________

# Start Building
## I have created a folder name as tera and a file to write all the Terraform in this file name as project4.tf .

![image](https://user-images.githubusercontent.com/61896468/95584090-c4cc7480-0a5a-11eb-823f-06dbd75a8168.png)

# Step-1 - create vpc
## First we need to create provider . The Amazon Web Services (AWS) provider is used to interact with the many resources supported by AWS. The provider needs to be configured with the proper credentials before it can be used.

# *Below Terraform code is to create aws VPC in which*

##  ``cidr_block - is, When we create a VPC, you must specify a range of IPv4 addresses for the VPC in the form of a Classless Inter-Domain Routing (CIDR) block; for example, 10.0. 0.0/16.``

![image](https://user-images.githubusercontent.com/61896468/95584263-078e4c80-0a5b-11eb-84f8-51e5e637abba.png)

# Step-2-a - create public subnet
## A public subnet is a subnet that's associated with a route table that has a route to an Internet gateway. A private subnet with a size /24 IPv4 CIDR block for example "192.168.0.0/24".

![image](https://user-images.githubusercontent.com/61896468/95584322-27be0b80-0a5b-11eb-809f-59607cf5a5d3.png) 

# Step-2-b - create private subnet

![image](https://user-images.githubusercontent.com/61896468/95584372-3f958f80-0a5b-11eb-9325-5f21986504bd.png) 

## now both the subnet are private, to make public one of the above subnet we need to create route table and Internet gateway for vpc and then associate to public subnet.

# Step-3 - create Internet gateway
## ``An internet gateway serves two purposes: to provide a target in your VPC route tables for internet-routable traffic, and to perform network address translation (NAT) for instances that have been assigned public IPv4 addresses.``

![image](https://user-images.githubusercontent.com/61896468/95584420-576d1380-0a5b-11eb-9326-7222e1749539.png) 

# Step-4 - create Routing table
## A route table contains a set of rules, called routes, that are used to determine where network traffic from your subnet or gateway is directed.

# *After creating route table associate it with the one of the subnet to make it public.*

![image](https://user-images.githubusercontent.com/61896468/95584474-6f449780-0a5b-11eb-832f-062aea402c72.png) 

# Step-5 - create Nat gateway
## NAT Gateway is a highly available AWS managed service that makes it easy to connect to the Internet from instances within a private subnet in an Amazon Virtual Private Cloud (Amazon VPC). Previously, you needed to launch a NAT instance to enable NAT for instances in a private subnet.

![image](https://user-images.githubusercontent.com/61896468/95584533-84b9c180-0a5b-11eb-9f9b-732ec4b27324.png) 

# Step-6 - create Routing table

![image](https://user-images.githubusercontent.com/61896468/95584580-9bf8af00-0a5b-11eb-91a5-2d6fae12de0c.png) 

# Step-7 - create security group and launch Wordpress instances

## `Below code is to create security group for wordpress.`

## A security group acts as a virtual firewall for your EC2 instances to control incoming and outgoing traffic.

![image](https://user-images.githubusercontent.com/61896468/95584646-b3379c80-0a5b-11eb-9b48-7032fd3b8d1a.png) 

# `Below code is to launch Worpress EC2 instances.`

![image](https://user-images.githubusercontent.com/61896468/95584708-c8acc680-0a5b-11eb-8b93-6d6dd420b4ce.png) 

# Step-8 - create security group and launch MySQL instances
## Below code is to create security group for MySQL.

![image](https://user-images.githubusercontent.com/61896468/95584777-dd895a00-0a5b-11eb-8c1f-a19f66e7541e.png) 

# `Below code is to launch MySQL database EC2 instances.`

![image](https://user-images.githubusercontent.com/61896468/95584850-f8f46500-0a5b-11eb-9d7c-e342a4a35014.png) 

# now initalise the tera tera directory using command.

#    <p align="center">Terraform init </p>    

![image](https://user-images.githubusercontent.com/61896468/95584926-188b8d80-0a5c-11eb-95ea-43bc60c7aa9f.png) 

# to run the code terraform apply -auto-approve

![image](https://user-images.githubusercontent.com/61896468/95584992-2fca7b00-0a5c-11eb-90f4-8672720a4c4f.png)

![image](https://user-images.githubusercontent.com/61896468/95585009-3953e300-0a5c-11eb-99c3-45d9bab1bfa0.png) 


# ```and good practise to see everything is configured as it is or not . on aws console we can check.```


# <p align="center"> VPC </p> 

![image](https://user-images.githubusercontent.com/61896468/95585115-6607fa80-0a5c-11eb-86e4-34f60f2db66a.png) 

# <p align="center">Private Subnet</p> 

![image](https://user-images.githubusercontent.com/61896468/95585169-7c15bb00-0a5c-11eb-992a-2d39e7204140.png)

 
 
# <p align="center">Public Subnet</p>

![image](https://user-images.githubusercontent.com/61896468/95585224-918ae500-0a5c-11eb-8517-5d486c36a919.png) 

# <p align="center">INTERNET GATEWAY </p>

![image](https://user-images.githubusercontent.com/61896468/95585392-cac35500-0a5c-11eb-873b-f5aa7cec8ef4.png) 

# <p align="center">ROUTING TABLE</p>

![image](https://user-images.githubusercontent.com/61896468/95585292-a9626900-0a5c-11eb-9a74-fc751b023a8c.png)
![image](https://user-images.githubusercontent.com/61896468/95585313-b1220d80-0a5c-11eb-960c-09bf88b24c7b.png)

# <p align="center">NAT GATEWAY </p>

![image](https://user-images.githubusercontent.com/61896468/95585451-df9fe880-0a5c-11eb-96f1-36df464a02f6.png)

![image](https://user-images.githubusercontent.com/61896468/95585499-f47c7c00-0a5c-11eb-91a6-76ee84ac52c1.png)

# <p align="center">ROUTING TABLE </p>

![image](https://user-images.githubusercontent.com/61896468/95585607-0d852d00-0a5d-11eb-94d1-5d2d4c7b99c1.png)

![image](https://user-images.githubusercontent.com/61896468/95585624-1544d180-0a5d-11eb-83a6-37687e9e3cb6.png)

# <p align="center">SECURITY GROUP </p>

![image](https://user-images.githubusercontent.com/61896468/95585693-3279a000-0a5d-11eb-824f-96cb61ce2be7.png) 

# <p align="center">INSTANCE </p>

![image](https://user-images.githubusercontent.com/61896468/95585746-47563380-0a5d-11eb-84ee-ded82c1e37c6.png) 

# now access the worpress using worpress public ip .

![image](https://user-images.githubusercontent.com/61896468/95585938-90a68300-0a5d-11eb-878d-07d4f086b952.png) 

# *and to connect Worpress with MySQL database we need instance id of MySQL .*

![image](https://user-images.githubusercontent.com/61896468/95585793-5c32c700-0a5d-11eb-8b58-ed24fd4ec7d9.png)
![image](https://user-images.githubusercontent.com/61896468/95585805-62c13e80-0a5d-11eb-834d-1f6e4255a09f.png)
# `This is the final web page of wordpress .`

![image](https://user-images.githubusercontent.com/61896468/95585866-7a002c00-0a5d-11eb-8594-10baf4dd946b.png) 
# <p align="center"></p>
