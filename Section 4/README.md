# Project 1: Simple CodeDeploy revision

- Simple CodeDeploy revision project for deploying new web content to a webserver tier

## Prequisites

- Provisioning of the CloudFormation template provided in Section 1
- IAM Roles for codedeploy and simple-instance-profile as described in section 1

## Step 1: CodeDeploy Application and Deployment Group setup

- Log in into the AWS Console and navigate to CodeDeploy page.
- Create Application
- Application Name: DemoApp
- Compute Platform: Compute Platform
- Deployment group namee: LinuxWebTier
- Environment configuration: Amazon EC2 instances; Key: Name, Value: LinuxWebServer
- Service role ARN: arn:aws:iam::123456789010:role/CodeDeployServiceRole

## Step 2: Build revision for the LinuxWebTier and Publish it to AWS

- Download Project 1 Resources.zip and unzip the folder.
- Take the content an place it in your local github repo
- open terminal, navigate to your local repo folder.
- Type the following command " aws deploy push --application-name DemoApp --s3-location s3://bucketname/project1.zip --ignore-hidden-files --source ."

## Step 3: Linux CodeDeploy Actual Deployment

- Before starting on the project it would effiecient to monitor the CodeDeploy deployment see what is going behind the face and the user would see.
- Open the monitor.html in a text editor e.g "Text wrangler". 
- Follow the comments written on the sides e.g " '<iframe id="iframe1" src="http://52.237.501.851"></iframe>    	<!-- insert the public Ip of the first EC2 Instance -->'  this indicates that you shall put your EC2 public ip in the src instead of 52.237.501.851 "
- Save the file and double click it to open a browser page which points to each monitor of each instance alongside the ELB with a message of "hello world ip-xxx-xx-xx-xx"

- Navigate to CodeDeploy page, click on DemoApp --> revisions --> then click to deploy revision
- After being prompted automatically to Deployment page, Just need to manually specify the Deployment group name by click on the tab and choose the deployment group created previously. 
- Once the deploy button pressed the page will be directed to the Deployment page, the status will show creadted but once the refresh logo pressed it will show in progress. To see how the Deployment is taking effct swtich to monitor.html page where you will see once the deployment takes effect on an instance the text will change to "Hello World" in bold font.

## Step 4: Windows CodeDeploy Actual Deployment

- Copy Project 1 windows resouces into a new directory/folder e.g "windows-codedeploy"
- From the command line navigate to the directory
- Insert the following command " aws deploy push --application-name DemoApp --s3-location s3://bucketname/WindowsProject1.zip --ignore-hidden-files --source .
- Login to the AWS console --> Navigate to CodeDeploy page --> click on DemoApp --> Create new deployment group
- Deployment group namee: WindowsWebTier
- Environment configuration: Amazon EC2 instances; Key: Name, Value: WindowsWebServer

- Modify the windows-monitor.html as indicated in the file when you open it with a text editor e.g "text wrangler"
- Open the windows-monitor.html in a browser --> Navigate to CodeDeploy page, click on DemoApp --> revisions --> then click to deploy revision
- After being prompted automatically to Deployment page, Just need to manually specify the Deployment group name by click on the tab and choose the deployment group created previously. 
- Once the deploy button pressed the page will be directed to the Deployment page, the status will show creadted but once the refresh logo pressed it will show in progress. To see how the Deployment is taking effct swtich to monitor.html page where you will see once the deployment takes effect on an instance the text will change.

## Step 5: Windows CodeDeploy Actual Deployment

