# Project 2 - Deploy a High-availability Web App using CloudFormation

Deploy a high-availability web app to a secure network with automated monitoring of CPU and Memory with CloudWatch.

## Architecture Diagram

![alt text](Architecture.png)

## Create Stack
Make sure app.zip exists in an S3 bucket and name passed in parameter. 
Sample source file in src folder

>./create.sh {Stack Name} CloudFormationTemplate/deploy.yml CloudFormationTemplate/parameters.json

## Update stack with update command.

>./update.sh {Stack Name} CloudFormationTemplate/deploy.yml CloudFormationTemplate/parameters.json

## Delete stack with 
> delete.sh {stack-name}
 
 
Connect to your private instance with [AWS Session manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-getting-started.html). Update launch config for custom scripts.

