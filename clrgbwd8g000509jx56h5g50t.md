---
title: "Terraform (IaC) Automation-End-to-End Project"
seoTitle: "Terraform (IaC) Automation-End-to-End Project"
seoDescription: "terraform aws project"
datePublished: Tue Jan 16 2024 12:26:53 GMT+0000 (Coordinated Universal Time)
cuid: clrgbwd8g000509jx56h5g50t
slug: terraform-iac-automation-end-to-end-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705495923837/aa45dfdc-1288-4e0b-b465-8b9cd61192fe.gif
tags: ec2, aws, devops, terraform, infrastructure-as-code, devsecops, iac

---

# Terraform ❓

Terraform is an IAC tool that helps DevOps teams automate various infrastructure tasks. One of Terraforms primary use cases is provisioning cloud resources. HashiCorp developed a cloud-agnostic, open-source provisioning tool written in the Go language.

# Why Terraform❓

Terraform Cloud offers remote state management, which securely saves and controls the state of your infrastructure, facilitating cooperation and preventing disputes. Terraform state files are encrypted at rest, and you can let specific teams and individuals to see these state files.

# Project Overview 📰

Using Terraform we are going to create AWS resources and we are monitoring the instances by cloud watch.

* If EC2 instances CPU reaches 75% load , Cloud watch will trigger the Auto scale.
    
* Once Auto scale triggered it will add one new instance in EC2.
    
* If 5 mins avg load CPU reduced to 50%, Auto scale delete the one instance.
    
* Auto scale Min instances = 2, Max=5, Desired=2
    
* And SNS will notify the Auto scale activity via Email.
    
* At Specific time in a day Auto Scale refresh the instance
    
* Load balancer will added for all instances while create
    
* load balancer connected two availability zone for High availability.
    

Project Link- GitHub: [https://github.com/karthick-dkk/Terraform](https://github.com/karthick-dkk/Terraform)

# Requirements: 📦

* AWS-CLI
    
* AWS Access Key and Secret key
    
* Terraform
    

## AWS-CLI 💻

⬇️Download the [AWS-CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

**Install aws-cli**

```bash
unzip awscliv2.zip   # unzip the files
```

```bash
sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update
```

**Verify the installation**

```bash
unzip awscliv2.zip && sudo ./aws/install
```

## Configure AWS-CLI

Get you AWS access keys from AWS, by navigate to IAM--&gt;user--&gt;security credentials --&gt;Add new keys.

> Note: user need below permissions for perform this tasks
> 
> 1. AWS EC2 full access
>     
> 2. AWS VPC full access
>     
> 3. AWS SNS full access
>     

```bash
[root@centos7 test-5]: aws configure

AWS Access Key ID [****************CCCD]: <your Access key>
AWS Secret Access Key [****************02V1]: <your Secret Key>
Default region name [ap-south-1]: <region>
Default output format [jq]:
```

# Install Terraform

Follow the below instructions for terraform [installation](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

**For Debian distributions**

configure hashiCorp gpg key

```bash
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common

wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg

gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint
```

Install terraform package

```bash
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update

sudo apt-get install terraform
```

check the `terraform --version` for verify.

## Download the Project files from GitHub

```bash
git clone https://github.com/karthick-dkk/Terraform 

cd Terraform/aws/projects/ec2
```

## Files Overview: 📜

`app_tfvars` - store the variables values.

`variables` - Assign the variable , type, default value

`main.tf` - Executable code file, modules

main.tf --&gt; variabels.tf --&gt; app\_tfvars --&gt; AWS API

You can modify the configurations as per your requirements.

# Run Terraform 🗃️

Initialize the terraform for download the required plugins

```bash
terraform init
```

## Test the config 🧪

```bash
terraform plan -var-file=app_tfvars
```

## Apply the config ⛈️

```bash
terraform apply -var-file=app_tfvars
```

*<mark>Note:</mark>*

*Do not remove terraform.tfstate files.*

*Terraform will save the current state, previous state , desired state on local file.*

*do not change the configurations from AWS console, once apply terraform , it will produce conflict error, then terraform will corrupt.*

### Delete the terraform config 🗑️

```bash
terraform destroy  -var-file=app.tfvars
```

---

Follow for more: ✌️

LinkedIn: [https://www.linkedin.com/in/karthick-dkk/](https://www.linkedin.com/in/karthick-dkk/)

Medium: [https://karthidkk123.medium.com/](https://karthidkk123.medium.com/)

Github: [https://github.com/karthick-dkk/](https://github.com/karthick-dkk/)

Hashnode: [https://karthick-dk.hashnode.dev/](https://karthick-dk.hashnode.dev/)

[Dev.to](http://Dev.to): [https://dev.to/karthickdkk](https://dev.to/karthickdkk)