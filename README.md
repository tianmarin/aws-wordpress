# aws-wordpress
This architecture provides best practices and a set of YAML CloudFormation templates for deploying WordPress on AWS.



__Production Environment__

* Enhanced Monitoring
* Backup Retention Period (7 days database retention period)
* Auto Minor Version Upgrade (No)
* Database Encryption (Yes)


* Master
	* AWS::CloudFormation::Stack
* VPC
	* AWS::EC2::VPC
	* AWS::EC2::Subnet
	* AWS::EC2::SubnetRouteTableAssociation
	* AWS::EC2::VPCGatewayAttachment
	* AWS::EC2::InternetGateway
	* AWS::EC2::EIP
	* AWS::EC2::NatGateway
	* AWS::EC2::Route
	* AWS::EC2::RouteTable
	* AWS::EC2::FlowLog :calendar:
* Security Groups
	* AWS::EC2::SecurityGroup
* Bastion
	* AWS::AutoScaling::AutoScalingGroup
	* AWS::AutoScaling::LaunchConfiguration
	* AWS::IAM::InstanceProfile
	* AWS::IAM::Role
* EFS
	* AWS::EFS::FileSystem
	* AWS::EFS::MountTarget
* RDS
	* AWS::RDS::DBCluster
	* AWS::RDS::DBInstance
	* AWS::RDS::DBSubnetGroup
* Web Servers
	* AWS::ECS::Cluster
	* AWS::ECS::TaskDefinition
	* AWS::ECS::Service

# Master Template
## Input Parameters

### System

* Production Eviroment

### AWS Parameters

* EC2 Key Name Pair

### Database Parameters

* Database Name
* Database Master Username
* Database Master Password
* Database Instance Class Type

# Bastion Template

__Resources__

* AutoScalingGroup


Que cosas quiero hacer:
* Configuración `motd`
* Instalación `git` para ajuste de plugins?
* Instalación `mysql` para utilizar MySQL utility para la conexión a la base de datos por consola (workaround)
* Instalar phpmyadmin??










---

Installs: git, mysql
Aliases
__Connection to Database__
The bastion host allows direct connection to query the wordpress database throught the MySQL utility. Keep in mind the bastion will be prepared for thie connection, however you will need the _rds master user password_.


To connect to the database using MySQL utility type:
`mysqlconn`


> __Note__

>`mysqlconn` is an alias for:

>`mysql -h [RDS_endpoint] --ssl-ca=/urs/local/rds-combined-ca-bundle.pem --ssl-verify-server-cert`

You will see output similar to the following:

```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 350
Server version: 5.6.10-log MySQL Community Server (GPL)

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

mysql>
```
