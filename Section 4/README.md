# Project 1: Simple CodeDeploy revision

## Purpose

- Simple CodeDeploy revision for deploying new web content to a webserver tier

## Prequisites

- Provisioning of the CloudFormation template provided in Section 1

## Step 1: CodeDeploy Application and Deployment Group setup

- Log in into the AWS Console and navigate to CodeDeploy page.
- Create Application
- Application Name: DemoApp
- Compute Platform: Compute Platform
- Deployment group namee: LinuxWebTier
- Environment configuration: Amazon EC2 instances; Key: Name, Value: LinuxWebServer
- Service role ARN: arn:aws:iam::123456789010:role/CodeDeployServiceRole

## Step 2: Build revision for the LinuxWebTier and Publish it to AWS
