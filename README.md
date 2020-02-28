# wordpressCloudFormation
RDS-VPC-EC2 on master template Cloud formation. 

Cloudformation: AWS CloudFormation is a service that helps you model and set up your Amazon Web Services resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and AWS CloudFormation takes care of provisioning and configuring those resources for you. You don't need to individually create and configure AWS resources and figure out what's dependent on what; AWS CloudFormation handles all of that. The following scenarios demonstrate how AWS CloudFormation can help. 

On this repo, we can found the structure to create a wordpress site on four templates. the structure has a secuential form, we use the master template to call the vpc, rds, and ec2 templates to create the site. You can check the code to undestand the way to do it. Yaml, is the code used to create the templates. 
