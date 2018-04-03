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
