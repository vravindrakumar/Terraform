Components in Terraform:

1.Providers
#Define the provider
provider "aws" {
  region = "us-west-2"
}

2.Resources:
#Define a resource (EC2 instance)
resource "aws_instance" "example"
ami      = "ami-0c55b159cbfafe1f0" #Example Amazon Linux 2AMI
 instace_type = "t2.micro"
 
 #Example of setting tags
 tags = {
  Name = "example-instance" {
}
3.Variable :
variable "aws_region" {
description  = "The AWS region to deploy resource in"
  type    = string
  default  ="us-west-2"
  
}
variable "instace_type" {
 description = "The type of EC2 instance"
 type        =    string

}
variable "ami_id" {
 description = " The AMI ID  for EC2 instance"
 type   = string

}

variable "instance_name" {
 description = "The name tag for the EC2 instance"
   type   = string
   default =" example-instance"
}
4.Statefile
terraform.tfstate

5.Provisioners:
a)Inline Provisioners
 i)local-exec
 ii)remote-exec
 resource "aws_instance" "example" {
 ami         = "ami-0c55b159cbfafe1f0"
 instace_type = "t2.micro"
  provisioner " local-exec" {
  command  = "echo $ {aws_instance.example.public_ip)
  
  }
 provisioner "remote-exec" {
 inline   = {
  "sudo apt-get update" ,
  "sudo apt-get install -y nginx" ,
  }
 
 }
 connection  {
   type  = "ssh"
   user  = "ubuntu"
   private_key = file( "~/.ssh/id_rsa")
   host        = self.public.ip {
    }
  }
 
}
 
 
b)File  Provisioners
resource "aws_instance" "example" {
  ami        = "ami-0c55b159cbfafe1f0"
  instace_type = "t2.micro"
  
  provisioner "file" { 
  source     = "my-app.conf"
  destination = "/etc/nginx/sites-available/my-app.conf"
  
  connection {
  type   = "ssh"
  user      = ubuntu
  private_key = file ("~/.ssh/id_rsa")
  host        = self.public.ip
  
     }
  }

}

VCS
Build automation
Testing
CI/CD
C.Deployment (Configuration Management)


6.Backend: (Remote Statefile)
  terraform {
 backend "s3" {
 bucket   = "my-terraform-state"
 key      = "path/to/my/key"
 region   = "us-west-2"
 encrypt  =  true
 dynamobd_table = "terraform-locks"
 
  }
}
---------------------------------
 terraform {
 backend "azurerm" {
 storage_account_name  = "myStorageAccount"
 container_name        = "tfstate"
 key                   = "terraform.tfstate"
 }
 
 }

-------------------------------------------
 terraform {
 backend "gcs" {
 bucket  = "my-bucket"
 prefix  = "terraform/state"
  
  }
}

 ------------------------------------------------
S3
Azure Blob
Google cloud Storage
Terraform cloud 