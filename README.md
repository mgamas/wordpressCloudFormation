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
   

## RDS Template [rds-mysql.yml] 💽 
the rds template creates the relational database, in this case, we create a MySQL database using the standard rds cloudformation. the purpose of the database is to store the WordPress site information, to allow that we need to open communication ports through a database security group. Check the code see more details about the template. 

***RDS Diagram***

![alt text](https://github.com/mgamas/wordpressCloudFormation/blob/master/rdsImage.PNG)

### parameters for vpc template.

> enviromentName:
  - Description: enviroment for all rds
  - Type: String

> dbClass:
  - Description: database instance class
  - Type: String
  - Default: db.t2.micro
    
> EngineVer:
  - Description: Version of the Engine of the DB.
  - Type: String
  
> dbName:
  - Description: database name
  - Type: String
  
> dbUserName:
  - Description: The WordPress database admin account username
  - Type: String
    
> dbPassword:
  - NoEcho: 'true'
  - Description: The WordPress database admin account password
  - Type: String

> DBAllocatedStorage:
  - Description: The size of the database (Gb)
  - Type: Number
  
> PrivateSubnet1:
  - Description: Subnet to allow communication for the rds
  - Type: String

> PrivateSubnet2:
  - Description: Subnet to allow communication for the rds, aws requests 2 subnets
  - Type: String
  
> vpcId:
  - Description: VPC name, the components for WordPress site has to be on the same vpc
  - Type: String
  
> secGroup:
  - Description: security group name, the templates need to receive an sg to create a DB security group
  - Type: String


## EC2 Template [EC2.yml] 💻
the EC2 template builds a virtual machine on the cloud and deploys the services needed to stand up the WordPress, like the apache web service. We use the user data property of the EC2 to configure the environment on the instance and configure the connection between the WordPress and the database located on rds. 


![alt text](https://github.com/mgamas/wordpressCloudFormation/blob/master/ec2Image.PNG)

### parameters for EC2 template. 

> dbName:
  - Description: database name
  - Type: String
  
> dbUserName:
  - Description: The WordPress database admin account username
  - Type: String

> dbPassword:
  -  Description: The WordPress database admin account password
  -  Type: String

> dbEndpoint:
  - Description: the rds string conection.
  - Type: String
    
> KeyName:
  - Description: Name of an existing EC2 KeyPair to enable SSH access to the instances
  - Type: 'AWS::EC2::KeyPair::KeyName'
  
> PublicSubnet1:
  -  Description: public subnet assignment to allow connection to the internet
  -  Type: String
  
> secGroup:
  - Description: EC2 security group name
  - Type: String
