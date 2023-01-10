# Attach-EBS-Volume

AWS provides storage in various forms, including Elastic Block Store (EBS) and Instance Store.

EBS volumes are durable and can survive instance crashes or terminations, whereas Instance Store volumes are ephemeral, meaning they exist only until the instance stops running. EBS provides block-level storage for storing data.

The usual pattern is to provision an EBS disk and attach it to an instance. Data gets stored on the EBS disk, which is mounted to the instance as a filesystem. When the instance is terminated for whatever reason, the EBS volume survives. We can attach this EBS volume to another instance should we need it.

In this lab, we will create an EBS volume and attach it to an instance. Note that we will not be formatting the disk or mounting the formatted disk on the instance in this lab.

# Learning Objectives

1. Create an EBS volume using the AWS CLI
2. Attach an EBS volume to an instance
3. Modify and delete an EBS volume
