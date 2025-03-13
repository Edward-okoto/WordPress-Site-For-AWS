# WordPress Site For AWS

### Project Scenario

A small and medium sized digital marketing agency "DigitalBoost" wants to enhance its online presence by creating a high performance wordPress based site for their clients. The agency needs a scalable, secure, and cost- effective solution that can handle increasing traffic and seamlessly integrate with existing infrastructure.

### Project Objective

Design and Implement a Wordpress Solution using various AWS services,such as Networking,Compute,Object storage and Databases.

## PRACTICAL

## VPC Set-Up

Create Virtual Private Network (VPC) to isolate and secure for the WordPress Infrastructure

* Login to AWS account and search for VPC and click VPC.


   ![](./img/wd1.png) 

* Name and define IP range for the VPC,then click `Create VPC`

   ![](./img/wd2.png) 


* Create VPC with public and private subnets.On the subnet    section,click `Create subnet`

   ![](./img/wd3.png)

## Create Subnets

* Public subnet 1.

  * Name = `Public_WordPress_01`

  * Choose the newly created Wordpress VPC

  * choose a CIDR of `10.0.0.0/28`

  * Choose availabilty zone of `eu-north-1a`

  Public subnet 2.

  * Name = `Public_WordPress_02b`

  * Choose the newly created Wordpress VPC

  * choose a CIDR of `10.0.0.16/28`

  * Choose availabilty zone of `eu-north-1b`

  Private subnet 1.

  * Name = `Private_WordPress_01a`

  * Choose the newly created Wordpress VPC

  * choose a CIDR of `10.0.0.32/28`

  * Choose availabilty zone of `eu-north-1a`

  Private subnet 2.

  * Name = `Private_WordPress_02a`

  * Choose the newly created Wordpress VPC

  * choose a CIDR of `10.0.0.48/28`

  * Choose availabilty zone of `eu-north-1a`

  Private subnet 3.

  * Name = `Private_WordPress_01b`

  * Choose the newly created Wordpress VPC

  * choose a CIDR of `10.0.0.64/28`

  * Choose availabilty zone of `eu-north-1b`

  Private subnet 4.

  * Name = `Private_WordPress_02b`

  * Choose the newly created Wordpress VPC

  * choose a CIDR of `10.0.0.80/28`

  * Choose availabilty zone of `eu-north-1b`

   ![](./img/wd4.png)
   ![](./img/wd5.png)
   
## Create Route tables

* Configure route table for each of the subnets.

  On the Route table section,click `Create route table`.

    
    ![](./img/wd6.png)

 
  Public Route table

   * Choose the name of the public subnets route table,and attach it to the created VPC and click `Create route table`

     ![](./img/wd7.png)

    * Choose `Subnet associations` and click `Edit subnet association`

      ![](./img/wd8.png)

    * Select the public subnets and click `Save associations`

      ![](./img/wd9.png)
      ![](./img/wd10.png)


  Private Route table

   * Choose the name of the private subnets route table,and attach it to the created VPC and click `Create route table`.

      ![](./img/wd11.png)
      ![](./img/wd12.png)

  * Choose `Subnet associations` and click `Edit subnet association`

    ![](./img/wd13.png)

    * Select the private subnets and click `Save associations`

    ![](./img/wd14.png)
    ![](./img/wd15.png)

## Create Internet Gateway

* Locate the `Internet gateway` section and click `Create internet gateway`

  ![](./img/wd17.png)
  ![](./img/wd18.png)

* Attach the Internet gateway to a VPC

   ![](./img/wd19.png)

* Select the created VPC for WordPress and click `Attach internet gateway`

     ![](./img/wd20.png)
      ![](./img/wd21.png)

* Select the Public route table,Edit the route and allow all subnets 0.0.0.0/0 and point it to the created `Internet gateway`

    ![](./img/wd22.png)
     ![](./img/wd23.png)


## Create a NAT gateway

 * Locate the NAT gateway section and click `Create nat gateway`

     ![](./img/wd24.png)

 * Choose a name for the nat gateway,choose a public subnet you want it connected to,allocate elastic IP and click Create.
      ![](./img/wd25.png)
      ![](./img/wd26.png)

* Edit the private route table and point it to the nat gateway.

  ![](./img/wd27.png)
  ![](./img/wd28.png)
  ![](./img/wd29.png)

## Set up EC2 instances and attach them to private subnets

* On the search bar, type EC2 and click on `EC2`

  ![](./img/wd30.png)

* Click on launch instance

  ![](./img/wd31.png)

* Create EC2 instances for WebServer and DatabaseServer.

   Webserver.
   * Name it Webserver
   * Choose Amazon Linux (ami)
   * Edit Network settings,select Wordpress VPC 
   * Select private network in eu-North-1a availability zone.

  ![](./img/wd32.png)
  ![](./img/wd33.png)

   DatabaseServer
   * Name it Databaseserver
   * Choose Amazon Linux (ami)
   * Edit Network settings,select Wordpress VPC 
   * Select private network in eu-North-1b availability zone.

  ![](./img/wd34.png)
  ![](./img/wd35.png)


  ![](./img/wd36.png)



## AWS MySQL RDS Setup

* Navigate to RDS:

  In the Services menu, search for RDS and select it.

  ![](./img/wd37.png)

* Create a Database:

  Click on Create database.

  ![](./img/wd38.png)

  Choose a Database Creation Method:

  Select Standard Create.

  Select Engine:

  Choose MySQL as the database engine.

  ![](./img/wd39.png)

  Specify DB Details:

  Engine version: Choose the desired version of MySQL.

  Templates: Select the appropriate template (e.g., Free tier, Production).

  Settings:

  DB instance identifier: Provide a unique identifier for your DB instance.

  ![](./img/wd40.png)

  Master username: Enter a username for the master user.

  Master password: Enter and confirm a strong password.

  ![](./img/wd41.png)

  DB Instance Size:

  Select the instance class based on your requirements (e.g., db.t2.microfor free tier).

  Storage:

  Configure the storage settings (e.g., allocated storage size, storage type).

   ![](./img/wd42.png)

  Connectivity:

  Virtual Private Cloud (VPC): Select the VPC in which to launch your DB instance.

  Subnet group: Choose the appropriate subnet group.

  ![](./img/wd43.png)

  Publicly accessible: Choose whether the DB instance should be publicly accessible.

  VPC security groups: Select or create security groups to allow inbound traffic to the DB instance.

  ![](./img/wd44.png)

  Additional Configuration:

  Database name: Specify a name for your initial database.

  Backup: Configure automated backup settings.

  Monitoring: Enable enhanced monitoring if needed.

  Maintenance: Set the preferred maintenance window.

  ![](./img/wd45.png)

  Create Database:
 
  Review the settings and click Create database.

  ![](./img/wd46.png)


  ## EFS Set-up for WordPress Files

  Create an EFS File System:

  Go to the Elastic File System (EFS) console in the AWS Management Console.

  ![](./img/wd47.png)

  Click Create file system.

  Provide a name for your file system,Choose WordPress VPC and click Customize and select the Performance mode (Standard or Max I/O).

  Choose the Throughput mode (Provisioned or Bursting).

  Select the Encryption settings if needed.

  ![](./img/wd48.png)
![](./img/wd49.png)

  Click Next.

  ![](./img/wd50.png)
  ![](./img/wd51.png)



  Create a Security Group for EFS:

  Go to the EC2 console and select Security Groups.

    ![](./img/wd52.png)

  Create a new security group and add inbound rules to allow NFS traffic from your EC2 instances.

    ![](./img/wd53.png)

  Create Mount Targets:

  In the EFS console, select your file system and click Create mount target.

  Choose the availability zones where your EC2 instances are located.

  Select the security group you created earlier.
    
    ![](./img/wd54.png)
  