provider "aws" {
  region = var.region
}

  resource "aws_instance" "web" {
  count = 2
  ami           = var.ami
  instance_type = var.int_type
 # subnet_id = "aws_subnet.pub_vpc.id"
 # security_groups = ["aws_security_group.sg.id"]
  
  tags = {
    Name = "Manojterraform"
  }
}

---------------------------------------------------


var.tf
  variable  "region" {
    type = string
    default = "us-east-1"
  }
  
  variable "ami" {
    type = string
	default = "ami-026b57f3c383c2eec"
}
	variable "int_type" {
	  type = string
	  default = "t2.micro"
	
}	
	

