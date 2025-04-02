# KCVPC-Networking

# Step 1: Create a VPC

### AWS Console Steps:
### Navigate to VPC Dashboard
### Click Create VPC
### Enter Name: KCVPC
### Set IPv4 CIDR: 10.0.0.0/16
### Click Create VPC


![Screenshot (18)](https://github.com/user-attachments/assets/8c3bcf8b-2806-4953-9b0a-42c983e05766)


# Step 2: Create Subnets
 ## Public Subnet
  ### Name: PublicSubnet
  ### CIDR Block: 10.0.1.0/24
  ### Availability Zone: Select any

![IMG-20250402-WA0005](https://github.com/user-attachments/assets/a4fe02cb-24a2-4263-94c3-b4577a8a26fd)

 ## Private Subnet
  ### Name: PrivateSubnet
  ### CIDR Block: 10.0.2.0/24
  ### Availability Zone: Same as PublicSubnet

 ## AWS Console Steps:
  ### Navigate to VPC Dashboard > Subnets
  ### Click Create Subnet
  ### Select KCVPC as VPC
  ### Add PublicSubnet with CIDR 10.0.1.0/24
  ### Add PrivateSubnet with CIDR 10.0.2.0/24
  ### Click Create

 ![Screenshot (19)](https://github.com/user-attachments/assets/7b7a9d0b-3d2f-4e16-8fc6-34e36d0e0791)

# Step 3: Configure Internet Gateway (IGW)

 ## AWS Console Steps:
  ### Navigate to VPC Dashboard > Internet Gateways
  ### Click Create Internet Gateway
  ### Name it KCVPC
  ### Attach it to KCVPC
 
![IMG-20250402-WA0007](https://github.com/user-attachments/assets/fc1e5066-5e6c-4456-a793-59562e6caae9)

![IMG-20250402-WA0009](https://github.com/user-attachments/assets/85f9b1fd-ef49-48ba-b555-d883a2cc92dd)

# Step 4: Configure Route Tables
 ### Public Route Table
 ### Name: PublicRouteTable
 ### Associate with: PublicSubnet
 ### Route: 0.0.0.0/0 → IGW

![IMG-20250402-WA0010](https://github.com/user-attachments/assets/48f74bbd-9d0b-4a93-bbcd-897a837001ec)

 ### Private Route Table
 ### Name: PrivateRouteTable
 ### Associate with: PrivateSubnet
 ### No direct internet access


![IMG-20250402-WA0012](https://github.com/user-attachments/assets/30fd3752-9439-4def-afe1-b8e87eb1d6ae)

 ### AWS Console Steps:
 ### Navigate to Route Tables
 ### Create PublicRouteTable & Associate with PublicSubnet

![IMG-20250402-WA0013](https://github.com/user-attachments/assets/e003d502-0fa2-4944-844f-5a99862a1c61)


 ### Add Route (0.0.0.0/0 → IGW)
 ### Create PrivateRouteTable & Associate with PrivateSubnet


![IMG-20250402-WA0014](https://github.com/user-attachments/assets/5ddf15f3-8a6c-4f26-a683-9814427366be)

# Step 5: Configure NAT Gateway
 ### Create a NAT Gateway in the PublicSubnet
 ### Allocate an Elastic IP for NAT Gateway
 ### Update the PrivateRouteTable to route 0.0.0.0/0 → NAT Gateway

![IMG-20250402-WA0015](https://github.com/user-attachments/assets/eaef0fdb-7704-4148-b0d2-1e4a14a3e9bf)

## AWS Console Steps:
 ### Navigate to NAT Gateway
 ### Click Create NAT Gateway
 ### Select PublicSubnet
 ### Attach an Elastic IP
### Update PrivateRouteTable with 0.0.0.0/0 → NAT Gateway

![IMG-20250402-WA0016](https://github.com/user-attachments/assets/f2a839d1-9099-42cb-a93a-9ceaee522c6e)


# Step 6: Set Up Security Groups
 ### Public Security Group (Web Servers)
 ### Allow HTTP (80) & HTTPS (443) from anywhere (0.0.0.0/0)
 ### Allow SSH (22) from your IP only
 ### Allow all outbound traffic

![IMG-20250402-WA0017](https://github.com/user-attachments/assets/17de9472-b296-478d-8502-345e8a7c6981)


 ### Private Security Group (Database Servers)
 ### Allow all outbound traffic
![IMG-20250402-WA0018](https://github.com/user-attachments/assets/c546945b-1be2-495e-8520-4946fcdd855b)


# Step 7: Configure Network ACLs (NACLs)
  ### Public Subnet NACL
  ### Inbound: Allow HTTP, HTTPS, and SSH
  ### Outbound: Allow all

![Screenshot (20)](https://github.com/user-attachments/assets/19dd8ee2-7a44-4329-9ed5-0e9808a34e47)

 ### Private Subnet NACL
 ### Inbound: Allow from PublicSubnet
 ### Outbound: Allow to PublicSubnet & Internet

![Screenshot (21)](https://github.com/user-attachments/assets/750fac81-166a-4726-8011-20b58bbdd139)


# Step 8: Deploy EC2 Instances
  ### Public EC2 Instance
  ### Launch an EC2 in PublicSubnet
  ### Attach Public Security Group
  ### Verify internet access

  ### Private EC2 Instance
  ### Launch an EC2 in PrivateSubnet
  ### Attach Private Security Group
  ###  Verify outbound access via NAT Gateway
 ![IMG-20250402-WA0021](https://github.com/user-attachments/assets/e8e07701-9d82-466f-bc3e-ccae188311f7)

![IMG-20250402-WA0020](https://github.com/user-attachments/assets/12bde306-5e20-4a66-9b82-6941d427d52d)

![IMG-20250402-WA0022](https://github.com/user-attachments/assets/f0b4f7e5-59ec-46c7-863e-93b1447c09ff)
