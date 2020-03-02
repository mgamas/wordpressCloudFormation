# wordpressCloudFormation 🚀
RDS-VPC-EC2 on master template Cloud formation. 

Cloudformation: AWS CloudFormation is a service that helps you model and set up your Amazon Web Services resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and AWS CloudFormation takes care of provisioning and configuring those resources for you. You don't need to individually create and configure AWS resources and figure out what's dependent on what; AWS CloudFormation handles all of that. The following scenarios demonstrate how AWS CloudFormation can help. 

![alt text](https://github.com/mgamas/wordpressCloudFormation/raw/master/imagen.png)

On this repo, we can found the structure to create a wordpress site split on four templates. the structure has a secuential form, we use the master template to call the vpc, rds, and ec2 templates to create the site. You can check the code to undestand the way to do it. Yaml, is the code used to create the templates. 

## MasterTemplate.yml 🛠️
The master template, has the task of receive the parameters needed and requested by the other templates that will be called since the master template. Logical the master makes the relationships betwen the other templates, doing the conections using inputs and outputs parameters.

### parameters for master template

>  KeyName:

- Type: 'AWS::EC2::KeyPair::KeyName'
- Description: Name of an existing EC2 KeyPair to enable SSH access to the instances
      
>  BucketName:

- Type: String
- Description: S3 buket name 

*** you can see detail about parameters on file comments. ***

## VPC Template [vpc.yml] ⚙️
the vpc template, creates the network cloud infraestructure to delivery services that alow wordpress to execute. The vpc present on this repository has six subnets, three private and three public, the private subnets handles the RDS, better know as relacional database service. The public subnets handles de EC2 instance allowed conections from the internet. the vpc has an internet gateway, and on the file you can found the security group, chek the file to see more details. 

***VPC Diagram***
![alt text](https://github.com/mgamas/wordpressCloudFormation/raw/master/vpcImage.png)

### parameters for vpc template.

> EnvironmentName:
   - Description: Prefix to tags of resourcer names
   - Type: String
   - Default: egVPC
  
> VpcCIDR:
   - Description: CIDR Notation for vpc
   - Type: String
   - Default: 10.0.0.0/16

 > PublicSubnet1CIDR:
   - Description: Ip range
   - Type: String
   - Default: 10.0.1.0/24

 > PublicSubnet2CIDR:
   - Description: Ip range
   - Type: String
   - Default: 10.0.2.0/24
  
 > PublicSubnet3CIDR:
   - Description: Ip range
   - Type: String
   - Default: 10.0.3.0/24

> PrivateSubnet1CIDR:
   - Description: Ip range
   - Type: String
   - Default: 10.0.4.0/24

> PrivateSubnet2CIDR:
   - Description: Ip range
   - Type: String
   - Default: 10.0.5.0/24

> PrivateSubnet3CIDR:
   - Description: Ip range
   - Type: String
   - Default: 10.0.6.0/24
   

## RDS Template [rds-mysql.yml] ⚙️
the vpc template, creates the network cloud infraestructure to delivery services that alow wordpress to execute. The vpc present on this repository has six subnets, three private and three public, the private subnets handles the RDS, better know as relacional database service. The public subnets handles de EC2 instance allowed conections from the internet. the vpc has an internet gateway, and on the file you can found the security group, chek the file to see more details. 

***VPC Diagram***
![alt text](https://github.com/mgamas/wordpressCloudFormation/raw/master/rdsImage.png)

### parameters for vpc template.

