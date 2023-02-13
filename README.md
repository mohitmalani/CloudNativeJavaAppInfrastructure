# infrastructure

**AWS Networking Setup**

	Here is what you need to do for networking infrastructure setup:

Create Virtual Private Cloud (VPC).
Create subnets in your VPC. You must create 3 subnets, each in a different availability zone in the same region in the same VPC.
Create an Internet Gateway resource and attach the Internet Gateway to the VPC.
Create a public route table. Attach all subnets created to the route table.
Create a public route in the public route table created above with destination CIDR block 0.0.0.0/0 and internet gateway created above as the target.
 

**Infrastructure as Code with CloudFormation**
	
	For this objective, you must complete the following tasks:

Install and set up AWS command-line interface.
Create CloudFormation template csye6225-infra.json or csye6225-infra.yml that can be used to set up required networking resources.
Values should not be hardcoded in your CloudFormation template.
You must be able to use the same CloudFormation template in the same AWS account and region to create multiple VPCs including all of its resources (listed in the “AWS Networking Setup” section) such as subnets, internet gateway, route table, etc.

**AWSCLI and Cloud Formation**

Configure your AWS profiles using below command:
> aws configure --profile=dev
> aws configure --profile=demo

Provide the access and secret keys along with region and output formats.


Below environment variables can be used to set the profile and region you want to work on:

> export AWS_PROFILE=dev
> export AWS_REGION=us-east-1

OR 
	--profile demo and --region us-east-2 can be used inline with aws command to set the profile and region.

Use below commands to create stack using cloudformation:

 1. Without Parameters:
	> aws cloudformation create-stack --stack-name myvpc-test --template-body file://csye6225-infra.yml

 2. With Parameter file:
	> aws cloudformation create-stack --stack-name my-vpc-a10 --template-body file://csye6225-infra.yml \
	--parameter file://param.json \
	--capabilities CAPABILITY_NAMED_IAM
					 
 3. With deploy command and parameters in json file:
        > aws cloudformation deploy --stack-name testStack --template-file csye6225-infra.yml --parameter-overrides file://param.json
	

--The yml file in the command contains the cloudformation template
					 

And to delete stack:
> aws cloudformation delete-stack --stack-name myvpc-a10


**AWS CLI Command to import SSL certificate**

> aws acm import-certificate --certificate fileb://prod_avinashraikesh_me.crt \
--certificate-chain fileb://prod_avinashraikesh_me.ca-bundle \
--private-key fileb://PrivateKey.pem

