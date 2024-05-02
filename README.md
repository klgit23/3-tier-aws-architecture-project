## Project Objective: build a 3-tier architecture on AWS
(from AOS Note project)
### Steps
* Create a vpc (Enbale dns host name in vpc) > create internet gateway and attach to vpc > create subnets, create route table, and associate route table with subnets
  - [x] Dev VPC: 10.0.0.0/16
  - [x] Public Subnet AZ1: 10.0.0.0/24
  - [x] Private App Subnet AZ1: 10.0.2.0/24
  - [x] Private Data Subnet AZ1: 10.0.4.0/24
  - [x] Public Subnet AZ2: 10.0.1.0/24
  - [x] Private App Subnet AZ2: 10.0.3.0/24
  - [x] Private Data Subnet AZ2: 10.0.5.0/24

 ![image](https://github.com/klgit23/terraform-proj1-v2/assets/154713258/a0566466-c6e9-4a5a-b723-71cde34b71f7)

* Create NAT gateway and allocate elastic IP

* Create security group:
  - [x] ALB SG: port=80 and 443, source=any ip
  - [x] Bastion host SG: port=22, source=laptop ip address
  - [x] Container SG: port=80 and 443, source= ALB SG
  - [x] Database SG: port=3306, source= Container SG and Bastion host SG

* Create MySQL RDS Instance; download and install Flyway; create databse table

* Create github personal token to access github
  
* Create a Dockerfile to build the docker image:
  build_image.ps1contains –build-arg GITHUB_USERNAME; because of information here, the file is in .gitignore file and kept off github repository; first `Set-ExecutionPolicy -ExecutionPolicy Unrestricted`; then build image locally in VS Code: `.\build_image.ps1`

* Create ECR for image storage:  
  - `aws ecr create-repository --repository-name REPONAME --region us-east-1` 
  - `docker tag aws_account_id aws_account_id.dkr.ecr. us-east-1.amazonaws.com/REPOSITORY:tag`
  - `aws ecr get-login-password --region us-east-1 | docker login –username`
  - `docker push aws_account_id.dkr.ecr.us-east-1.amazonaws.com/`

* Creat a Key Pair in AWS to log into a Bastion Host with EC2
* Create target group before creating a ALB; regisger targets and define listener and routing rules
  <img src="https://github.com/klgit23/terraform-proj1-v2/assets/154713258/6009940a-3975-4837-b9f4-5a8cf99e7408" width="60%">

* Create ECS by create a role for ecs-> define ecs task ->create a ecs service -> create a deployment
  <img src="https://github.com/klgit23/terraform-proj1-v2/assets/154713258/c82d0983-6a16-43b7-8918-5c9a2144caab" width="60%">

  <img src="https://github.com/klgit23/terraform-proj1-v2/assets/154713258/24c34161-fd0a-44f8-9be6-cf1b1d66e6b1" width="60%">

  <img src="https://github.com/klgit23/terraform-proj1-v2/assets/154713258/d7cf0fa1-28b1-47b0-8538-45be53ac14f4" width="60%">





 




