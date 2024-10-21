provider "aws" {
  region     = "ap-south-1"
  access_key = "my-access-key"
  secret_key = "my-secret-key"
}

 #Create VPC
resource "aws_vpc" "VPC01" {
  cidr_block       = "10.0.0.0/16"
  instance_tenancy = "default"

  tags = {
    Name = "main"
  }
}

 #Create subnet01
 resource "aws_subnet" "Subnet01" {
  vpc_id     = aws_vpc.VPC01.id
  cidr_block = "10.0.10.0/24"
  availability_zone = "ap-south-1a"
  tags = {
    Name = "Subnet01"
  }
}
 
 #Create Subnet02
resource "aws_subnet" "Subnet02" {
  vpc_id     = aws_vpc.VPC01.id
  cidr_block = "10.0.20.0/24"
  availability_zone = "ap-south-1b"

  tags = {
    Name = "Subnet02"
  }
}

 #Create Internet Gateway
resource "aws_internet_gateway" "IGW-VPC01" {
 vpc_id = aws_vpc.VPC01.id
 tags   = {
 Name   = "IGW-VPC01"
 
   }
}

 #Create Route Table
 resource "aws_route_table" "RT-VPC01" {
 vpc_id = aws_vpc.VPC01.id
 tags   = {
 Name   = "RT-VPC01"
 
   }
}

 #Create route to Internet Gateway
 resource "aws_route" "internet_route" {
 route_table_id = aws_route_table.RT-VPC01.id
 destination_cidr_block = "0.0.0.0/0"
 gateway_id  = aws_internet_gateway.IGW-VPC01.id

 }
  #Associate Subnet01 in RT-VPC01
  resource "aws_route_table_association" "a" {
   subnet_id  = aws_subnet.Subnet01.id
   route_table_id =aws_route_table.RT-VPC01.id
}

  #Associate Subnet02 in RT-VPC01
  resource "aws_route_table_association" "b" {
   subnet_id  = aws_subnet.Subnet02.id
   route_table_id =aws_route_table.RT-VPC01.id
}
