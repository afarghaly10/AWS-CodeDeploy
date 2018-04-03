# Prequisites and Setups
This Lesson is designed for setting up the initial requirements for AWS CodeDeploy.  

## Requirements 

 - Requirement 1 - S3 Bucket and Github Repo
 - Requirement 2 - IAM isntance profile and service roles
 - Requirement 3 - A web server tier (Windows + IIS)
 - Requirement 4 - A web server tier (Linux + Apache)

## Requirement 1

- To get started, log in or signup to your AWS account. Go to S3 page and create a new bucket.
- choose the bucket name to be "yourchoice -codedeploy" for convenience of use of the policy or you can edit the policy attached to your s3 bucket name.

- create or sign in to your GitHub account. Create a repo and give it a name of your choice.
- clone the repo to locally using the terminal or powershell by excuting '$ git clone "ur of your repo" '

## Requirement 2

- Create IAM service role for CodeDeploy service to use as well as 2 instance profiles; 1 simpler instances for project 1 and a more complex/Advanced instance profile for project 3.
- It is preferable also to create an additional IAM user to use with the integration with github.

### Creation of IAM service role for CodeDeploy Service

- Go to your AWS console then click on Roles. 
- Click on create role, choose AWS services, then pick CodeDeploy and create the role

### Creation of Simple Instance Profile

#### Creation of a policy for the role has to be done before creating the role itself.

- Go to your AWS console, Policies, create a policy, JSON.
- Click create a policy, choose JSON.
- Open the Simple-CodeDeploy-Instance-Profile-Policy file with a text editor and copy and past the policy in the JSON document in the policy area in AWS. 
- Click on Review policy, name it e.g "SimpleCodeDeployInstanceProfilePolicy" and create.

#### Simple Instance Profile Role Creation

- Go to your AWS console then click on Roles. 
- Click on create role, choose AWS services, then pick EC2.
- Attach the recently created policy to the role. 
- Name the Role e.g "SimpleCodeDeployInstanceProfile".


### Creation of Advanced Instance Profile

#### Policy Creation for Advanced Instance Profile

- Go to your AWS console, Policies, create a policy, JSON.
- Click create a policy, choose JSON.
- Open the Advanced-CodeDeploy-Instance-Profile-Policy file with a text editor and copy and past the policy in the JSON document in the policy area in AWS. 
- Under Resource changne the "yourname" to your s3 bucket name e.g if my bucket name is xyz-codedeply then the arn will be "arn:aws:s3:::xyz-codedeploy"
- Click on Review policy, name it e.g "AdvancedCodeDeployInstanceProfilePolicy" and create.

#### Advanced Instance Profile Role Creation

- Go to your AWS console then click on Roles. 
- Click on create role, choose AWS services, then pick EC2.
- Attach the recently created policy to the role. 
- Name the Role e.g "AdvancedCodeDeployInstanceProfile".


### Creation of IAM user specifically for GitHub

- Create an IAM user in the AWS console and give it programmatic access.
- Attach "AWSCodeDeployDeployerAccess" managed policy to the user
- Save the credentionals to your local computer.

## Requirement 3 and Requirement 4 (Infrastructure Setup)

### Both requirements 3 and 4 are already setup in the cloudformation template (CodeDeploy-Infrastructure) in this lesson. 

#### This template includes setting up web autoscaling,launch configs, ELBS, Security Groups to be used to host the application for CodeDeploy. 

##### Walkthrough the parameters:

- Stack name: Choose a stack name e.g infrastructure
- AZ: choose 3 availability zones e.g us-east-1a,us-east-1b,us-east-1c
- InstanceProfile: is the arn of the SimpleCodeDeployInstanceProfile e.g arn:aws:iam::123456789010:instance-profile/SimpleCodeDeployInstanceProfile
- InstanceType: It is recommended to use to t2.medium so it would be able to handle the windows instances but can choose t2.micro if want to have no charge if in free tier period.
- KeyName: your ec2 key pair
- LinuxAMIID: just the newest linux ami e.g ami-1853ac65 
- myIP: your IP address in CIDR notation
- PublicSubnets: your subnets for the picked AZ's e.g subnet-1dp75e48,subnet-1mb39f30,subnet-16438e88
- VPCID: your vpcid  e.g vpcid-1dp45e72 
- WindowsAMIID: use the community AMI and choose a windows AMI which is provided by amazon, so it has cli built in it, and also has iis e.g ami-31029d4b


## That is the END of this Lesson 


