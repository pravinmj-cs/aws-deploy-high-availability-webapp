
## Scenario
Your company is creating an Instagram clone called Udagram. Developers pushed the latest version of their code in a zip file located in a public S3 Bucket.
You have been tasked with deploying the application, along with the necessary supporting software into its matching infrastructure.
This needs to be done in an automated fashion so that the infrastructure can be discarded as soon as the testing team finishes their tests and gathers their results.


# Network Stack

## 1. Setup VPC, Internet Gateway and Gateway Attachment 

### Architecure Diagram

![alt text](images/nw-01-vpc.png)

### Resources and Outputs

![alt text](images/nw-03-resources.png)
![alt text](images/nw-04-outputs.png)

## 2. Setup Public and Private subnets inside VPC and interconnect with NAT Gateway and its  Route table association

### Architecture Diagram

![alt text](images/nw-final-arch.png)

### All Resources needed for network stack

![alt text](images/nw-05-all-resources.png)

### Final Outputs of network stack

![alt text](images/nw-06-all-op.png)

# S3 and IAM
### 3. Upload a web app zip to an S3 bucket

![alt text](images/upload-app-zip.png)

## 3. Create an Instance Profile for IAM

### IAM resources with relevant policies to access the S3 bucket

![alt text](images/iam-resources.png)

### IAM outputs

![alt text](images/iam-output.png)

# Server Stack

## 5. Setup Autoscaling Security groups, Load balancer with Launch Configurations and target groups and test deployment

- Deploy the static site created in [previous project](https://github.com/pravinmj-cs/aws-static-site) with Load balancer, listener and target groups with health check. An optional conditional was added to choose instance types for different environments using Conditions and !If function. We use t2.micro if its of development environment type and t3.small if it is of production environment
- Deploy with KeyName property in Public Cloud initially for debugging and to check if the IAM role can **get** values from **SSM parameter store**. Deployment and getting parameter was successful.
- Then the Keyname property was removed and deployed into Private subnet

### Architecture Diagram Update
![alt text](images/public_app_diagram.png)

### Load Balancer, Health check and target group

#### Tested with Public network with development environment

![alt text](images/lb.png)
![alt text](images/initial_cap.png)

#### Moved to private network, updated EnvironmentType to production environment and update autoscaling policy

![alt text](images/private-net-app.png)
![alt text](images/autos.png)

#### Update stack to include Cloud watch metrics to monitor CPU and Memory

![alt text](images/cwm.png)
![alt text](images/cwm2.png)

#### Load Balance Output HTTP URL
![alt text](images/http_url.png)

#### Tried to connect with Session Manager after updating stack to install ssm agent and updating instance profile policy
![alt text](images/sm.png)

#### Hosted Site
![alt text](images/website.png)

Scaled down instances and update environment type to run as development to avoid charges. 

Arrange namespaces and template formats, Removed Stack and tested one full recreation
Please refer to the hosted [link](http://udagr-webap-y6f31c66k93r-1021377290.us-east-1.elb.amazonaws.com/)


