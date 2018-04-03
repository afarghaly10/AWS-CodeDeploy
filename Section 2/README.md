# CodeDeploy Revisions 

This section is about trial of the initial setup resources for preparation for CodeDeploy revisions, structures and publishing. In this section I will not use the EC2 instances created in Section 1 as I will be needing these for the projects


## Chapters

 - Chapter 1 - Creating an Application 
 - Chapter 2 - Recommendations for structure and publishing
 - Chapter 3 - Walkthrough manual Publishing (S3 & Github Repo) via Console
 - Chapter 4 - Walkthrough revision deployment (S3 & Github) via CLI

## Chapter 1

- Log in the AWS console and navigate to the CodeDeploy page.
- Click on Get Started, for first time users, or create application; choose custom Deployment
- Choose an application name e.g "DemoApp" and EC2/On-premises as compute platform option. Pick any name for Deployment group name e.g "DemoAppWebTier"
- In Environment configuration section choose Amazon EC2 instances tab; as this is only to practice the best practice of revision I didn't want to use the instances so I choose the following Tag type:
Key = " Name"        Value = "LinuxWebTier"
- Under Service role ARN choose the CodeDeployServiceRole created in the section 1

## Chapter 2

### Recommendations for Structure and Publishing 

#### Structure

- Use AppSpec as a blueprint 
- Best practice is to use "scripts/" and "files/" folders within CodeDeploy revisions 
- appspec.yml must be in the root of the revision

#### Publishing

- Manual process overview; Compress the revision content as tar.gz or .zip then copy it to AWS S3 or GitHub. Lastly excute cli coomand to associate that CodeDeploy revision with a given application 
- Best practice is to use AWS CLI.

## Chapter 3 

### Requirements before using doing the Chapters 3 & 4 steps

- Open The command prompt and navigate to the local CodeDeploy Github directory 
- Download Section 2 Resource file; Unzip and place the files and folders in the local Github directory.

#### a) Deploying Revision from S3 via Console

- In the command prompt type "tar cvf demoRevision.tar* " from the root folder to create tar file of the revision contents 
- Copy this demoRevision.tar to S3 by inserting the command " aws s3 cp demoRevision.tar s3://buketname/ "
##### - Associate this CodeDeploy revision with CodeDeploy application 
- There are 2 Sperate permissions involved with deploying in CodeDeploy provision for the first time. The first is register application revision ,(which what is shown in the following steps), and the second is the actual deployment of the application.
- Go to the AWS Console then navigate to CodeDeploy page
- In the Deployment Groups created "DemoAppWebTier" click on deploy new revision
- Revision Type: my application is stored in S3
- Revision Location: s3://bucketname/objectname.tar
- Click on Deploy Now which will register the application revision

#### b) Deploying Revision from GitHub via Console
 
- Add the CodeDeploy revision to the repo using the following commands: i) "git add -A" ii) 'git commit -m "adding revision to repo" ' iii) git push 
- Go to the AWS Console then navigate to CodeDeploy page
- In the Deployment Groups created "DemoAppWebTier" click on deploy new revision
- Revision Type: my application is stored in GitHub
- Press on "Connect with GitHub" button and enter your credentials 
- Repository Name: username/repo-name
- Commit ID: last commit or revision commit id
- Click on Deploy Now which will register the application revision

## Chapter 4

#### a) Deploying Revision from S3 via CLI

- In the command prompt use the following command " aws deploy register-application-revision --application-name DemoApp --s3-location bundleType=" object extension, e.g tar",etag=" the etag of the object in the s3",bucket="bucketname",key="name of the object in s3 e.g demoRevision.tar"

#### b) Deploying Revision from GitHub via CLI

- Make a minor change to generate a new commit Id like for example "touch fakefile.txt"; "git add -A"; "git commit -m 'minor change'"; "git push"
- Copy the new commit ID
- In the command prompt use the following command " aws deploy register-application-revision --application-name DemoApp --github-location commitid="paste the copied commit id",repository="username/repo-name"

## Conclusion 

### Revision Deployment best practice is to publish, bundle and register the application revision on one command. This can be done via the following command
- "aws deploy push --application-name DemoApp --ignore-hidden-files --s3-location s3://bucketname/objectname --source . "


# That is the END of this Section 



