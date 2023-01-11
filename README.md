# Attaching an EBS Volume to an Instance

AWS provides storage in various forms, including Elastic Block Store (EBS) and Instance Store.

EBS volumes are durable and can survive instance crashes or terminations, whereas Instance Store volumes are ephemeral, meaning they exist only until the instance stops running. EBS provides block-level storage for storing data.

The usual pattern is to provision an EBS disk and attach it to an instance. Data gets stored on the EBS disk, which is mounted to the instance as a filesystem. When the instance is terminated for whatever reason, the EBS volume survives. We can attach this EBS volume to another instance should we need it.

In this lab, we will create an EBS volume and attach it to an instance. Note that we will not be formatting the disk or mounting the formatted disk on the instance in this lab.

# Objectives

1. Create an EBS volume using the AWS CLI
2. Attach an EBS volume to an instance
3. Modify and delete an EBS volume

### Create an EBS volume using the AWS CLI
The first of our scripts handles the prerequisites, creating a VPC, security group, rules, keys, and so on.
```bash
source ./1_create_resources.sh
```
Once the resources have been created, let's create an instance by executing the below script:
```bash
source ./2_create_instance.sh 
```
### Creating a Volume Using the AWS CLI

In the CLI, we use the create-volume command on the ec2 service to create a volume. We provide a few parameters, such as the size of the disk and availability zone. We can also provide the volume type.
However, we need to make sure we create the volume in the same availability zone as our instance. We can do so by executing the describe-subnets command:
```bash
AVAILABILITY_ZONE=`aws ec2 describe-subnets --subnet-id $SUBNET_ID --query 'Subnets[].AvailabilityZone' --output text`

echo The availability zone of the instance is: $AVAILABILITY_ZONE
```
