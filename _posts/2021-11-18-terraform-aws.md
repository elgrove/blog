---
layout: post
title: "Using Terraform to provision an AWS EC2 instance"
description: 
summary: 
---

The Apple Silicon M1 chips basically have two good options for VMs - either use Parallels 17 for wonderful virtualisation blended with the MacOS host, or UTM for classic virtualisation. Unfortunately, UTM doesn't expose an API and so can't be used with a VM provisioning tool like Terraform. So AWS it must be for my first go with Terraform!

First things first, I installed Terraform, then the `aws` command line interface and give it your access keys.

```
brew install awscli
aws configure
```

Next, I added the config from Hashicorp's own Terraform-AWS tutorial and changed the default region to eu-west-2 and changed the AMI to one suitable for that region, as AMIs are region-specific.

```
# main.tf
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.27"
    }
  }

  required_version = ">= 0.14.9"
}

provider "aws" {
  profile = "default"
  region  = "eu-west-2"
}

resource "aws_instance" "app_server" {
  ami           = "ami-0fdf70ed5c34c5f52"
  instance_type = "t2.micro"

  tags = {
    Name = "FirstGo"
  }
}
```

Once this is done, I can do the following

```
# initialise tf in the directory
terraform init
# format the config
terraform fmt
# validate the config
terraform validate
```

Success! the configuration is valid.


Lastly, `terraform apply` will print the actions to be taken for me to check and prompt for a confirmation.

First time I entered this, I got an error, I'm not sure why though because I have my AWS access keys set up!

```
error configuring Terraform AWS Provider: error calling sts:GetCallerIdentity: SignatureDoesNotMatch: The request signature we calculated does not match the signature you provided. Check your AWS Secret Access Key and signing method.
```

Weirdly, it work if I hard-code the keys in the main.tf, it works fine. My AWS keys are in the `~/.aws` directory and my understanding is that Terraform is supposed to collect them from there, but it hasn't in my case.

I run `terraform apply` and  type yes to confirm and that's it! The EC2 instance has been created.

To destroy, simply enter `terraform destroy`