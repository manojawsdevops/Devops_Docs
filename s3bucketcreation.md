provider "aws" {
  region = "us-east-1"
}

  resource "aws_s3_bucket" "b" {
  bucket = "manoj1411"

  tags = {
    Name        = "My bucket"
    
  }
}

resource "aws_s3_bucket_acl" "example" {
  bucket = aws_s3_bucket.b.id
  acl    = "private"
}
