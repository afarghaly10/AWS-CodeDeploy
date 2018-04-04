# Apps, Deployment Groups, and Deployment Configurations

 - In this Section a theoritical explaination of apps, Deployment Groups, and Deployment Configurations and why they are important before doing the practical steps.
 
 ## Why this section is important ?
 
  - Apps, Deployment Groups, and Deployment Configurations control how CodeDeploy works across multiple instances that comprise your system.
  
  ## Definittions:
  
  ### a) Application
  
 - " A name that uniquely identifies the application that you want to deploy. AWS CodeDeploy uses this name to ensure that the correct combination of revision, deployment configuration, and deployment group are being referenced during a deployment."
  
      AWS Documentation 
      
 - The application itself is Arbitrary you don't necessary need to have all of your tiers of a given application within one CodeDeploy application. You could have each one with its own application or similarly you could have multiple applications bundled under one application within CodeDeploy. 
 - Limit of 40 per region per account
 - Limit of 10 deployment groups
 
 ### b) Deployment Groups
 
 - " A set of individual instances. A deployment group contains indiviually-tagged instances, Amazon EC2 instances in Auto Scaling groups, or both."
      
      AWS Documentation
 
 #### Methods of Defining Deployment Groups 
 
 ##### i) EC2 Tage Based
 
 - No logic, only ad-hoc deployents
 - Use cases: Maintenance, one-time deployments
 
 ##### ii) ASG Group Based
 
 - Binds to Auto Scaling Lifecycle
 - Use cases: Patching, CodeDeploy driven app deployments
 
 ### c) Deployment Configurations
 
 - " A set of deloyment rules and deployment success and failure conditions that AWS CodeDeploy uses during a deployment." 
     
     AWS Documentation
     
#### Deployment Configurations Types     

##### a) Default Configurations 

- CodeDeploy.Default.OneAtATime
- CodeDeploy.Default.AllAtOnce
- CodeDeploy.Default.HalfAtATime

##### b) Custom Configurations

- Unique name
- Host count or fleet percent
- Value

## Practical Walkthrough for Apps, Deployment Groups, and Deployment Configurations

### a) App and Deployment Groups creation via the AWS console

- Login into the AWS console and reassure  that the EC2 instances, Auto Scaling groups provisioned in section 1 are up and functioning
- Navigate to CodeDeploy Page and create application
- Application Name: DemoApp2
- Compute Platform: Compute Platform
- Deployment group namee: LinuxWebTier
- Environment configuration: Amazon EC2 instances; Key: Name, Value: LinuxWebServer
- Service role ARN: arn:aws:iam::123456789010:role/CodeDeployServiceRole

#### once an application is created a subsequent deployments groups can be created
- Click on create new deployment group
- Deployment group name: WindowsWebTier
- Environment configuration: This time I will choose Auto Scaling group as a change. Name: Windows auto scaling group name e.g "CodeDeploy-Infrastructure-WindowsWebASG-1LNRG6QKLAV27"
- Service role ARN: arn:aws:iam::123456789010:role/CodeDeployServiceRole

### b) Deployment Configuration creation via the CLI

 - Open a terminal and navigate to the repo folder
 
 #### i) For minimum healty host with a percent 
 
 - Type the following command " aws deploy create-deployment-config --deployment-config-name 10Percent --minimum-healthy-hosts value=10,type=FLEET_PERCENT" 
 
 #### ii) For minimum healty host with an integer
 
- aws deploy create-deployment-config --deployment-config-name 7Hosts --minimum-healthy-hosts value=7,type=HOST_COUNT

#### iii) To Delete the Deployment Configuration use the following command

- aws deploy delete-deployment-config --deployment-config-name 7Hosts
- aws deploy delete-deployment-config --deployment-config-name 10Percent


# This is the END of this Section
















