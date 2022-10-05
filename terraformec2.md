provider "aws" {
  region = "us-east-1"
}

  resource "aws_instance" "web" {
  ami           = "ami-026b57f3c383c2eec"
  instance_type = "t2.micro"
 # subnet_id = "aws_subnet.pub_vpc.id"
 # security_groups = ["aws_security_group.sg.id"]
  
  tags = {
    Name = "Manojterraform"
  }
}

  resource "aws_vpc" "vpc" {
  cidr_block = "192.168.0.0/16"
  instance_tenancy = "default"
  
  
  tags = {
    Name = "Vpc_demo"
  }
  
}

  resource "aws_subnet" "pub_vpc" {
  vpc_id     = aws_vpc.vpc.id
  cidr_block = "192.168.1.0/24"

  tags = {
    Name = "public_vpc"
  }
}

  resource "aws_subnet" "private_vpc" {
  vpc_id     = aws_vpc.vpc.id
  cidr_block = "192.168.3.0/24"

  tags = {
    Name = "private_vpc"
  }
}

 resource "aws_security_group" "sg" {
  name        = "first sg"
  description = "Allow TLS inbound traffic"
  vpc_id      = aws_vpc.vpc.id

  ingress {
    description      = "TLS from VPC"
    from_port        = 22
    to_port          = 22
    protocol         = "tcp"
    cidr_blocks      = [aws_vpc.vpc.cidr_block]
  }

  egress {
    from_port        = 0
    to_port          = 0
    protocol         = "-1"
    cidr_blocks      = ["0.0.0.0/0"]
  }

  tags = {
    Name = "first sg"
  }
}

