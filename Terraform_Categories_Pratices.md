1.Create VPC with below CIDR
CIDR:10.0.0.0/16
VPC Name :VPC01

2.Create below Public Subnets
A)Subnet :1
Name:Subnet01
CIDR:10.0.10./24
Availability Zone: AZ1

B)Subnet02
Name:Subnet01
CIDR:10.0.20.0/24
Availability Zone:AZ2

3.Create Route Table
 Name :RT-VPC01
 
4.Create Internet Gateway in VPC01
  Name:IGW-VPC01
5.Add Internet route in RT-VPC01

6.Add Subnet01 & Subnet02