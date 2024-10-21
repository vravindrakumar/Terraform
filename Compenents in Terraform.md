Compenents in Terraform:
1.Providers
#Define the Providers
Provider "aws" {
  region = "us-west-2"
 }
#Define a resource (EC2 instance)
resource "aws _instance" "example" {
 ami    = "ami_0c55b159cbfafe1f0" # Example Amazon Linux 2 AMI
   instance_type = "t2.micro"
   # Example of setting tags
   tags = {
   Name = "example-instance"
   }
  }
  2.Resource:
  #Define a resource (EC2_instance)
 resource "aws_instance" "example" {
   ami       = "ami-oc55b159cbfafe1f0" # Example Amazon Linux 2 AMI
   instance_type = "t2.micro"
   #Example of setting tags
    tags = {
	 Name = "example-instance"
	}
}

3. Variable :
variable "aws_region" {
  description = "The AWS  region to deploy resource in"
   type       = string
   default    = "us-west-2"
  }
  variable "instance_type" {
   description = "The type of EC2 instance"
   type        = string
   default     = "t2.micro"
  }
  
  4.Statefile
  terraform.tfstate
  
  5.Provisioners:
  
  a)Inline Provisioners
  i)local-exec
  ii)remote-exec
 resource "aws_instance" "example"{ 
 ami       = "ami-oc55b159cbfafe1f0"
 instance_type = "t2.micro"
 
 provisioners " local-exec" { 
 command = "echo ${aws_instance.example.public_ip}"
  }
  
  provisioners "remote-exec" {
  inline  =  {
  "sudo apt-get update",
  "sudo apt-get install -y nginx",
  }
  connection {
  type      = "ssh"
  user       =  "ubuntu"
  private_key = file {"~/.ssh/id_rsa"}
  host        = self.public_ip
  
    }
  
  }
  
} 
 
  
  
  b) File Provisioners
  
  VCS
  Build automation
  Testing
  CI / CD
  C.Deployment ( Configuration Management) Ansible ,chef
 6.Backends : (Remote statefile)
 
  terraform {
  backend "s3" {
  bucket    = "my-terraform-state"
  key       =  "path/to/my/key"
  region    =  "us-west-2"
  encrypt   =   true
  dynamodb  = " terraform-locks"
  
 }
}
---------------------------------------
terraform
 backend "local" { 
 path = "relative/path/to/terraform.tfstate" 

  
   

