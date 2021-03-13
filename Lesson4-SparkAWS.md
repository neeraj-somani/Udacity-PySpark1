## notes from lesson 4

Lesson Overview
By the end of the lesson, you will be able to:

Distinguish between setting up a Spark Cluster using both Local and Standalone Mode
Set up Spark Cluster in AWS 
Use Spark UI
Use AWS CLI
Create EMR using AWS CLI
Create EMR Cluster
Test Port Forwarding
Use Notebooks on your Spark Cluster
Write Spark Scripts
Store and Retrieve data on the Cloud
Read and Write to Amazon S3
Understand the distinction between HDFS and S3
Reading and Writing Data to HDFS

### Overview of the Set up of a Spark Cluster
Amazon S3 will store the dataset.
We rent a cluster of machines, i.e., our Spark Cluster, and iti s located in AWS data centers. We rent these using AWS service called Elastic Compute Cloud (EC2).
We log in from your local computer to this Spark cluster.
Upon running our Spark code, the cluster will load the dataset from Amazon S3 into the cluster’s memory distributed across each machine in the cluster.
New Terms:
Local mode: You are running a Spark program on your laptop like a single machine.
Standalone mode: You are defining Spark Primary and Secondary to work on your (virtual) machine. You can do this on EMR or your machine. Standalone mode uses a resource manager like YARN or Mesos.

Local mode means Spark is running on your local machine. Standalone mode is distributed and uses resource management like Yarn or Mesos.

## Spark Cluster Managers
- Standalone Mode - mostly good enough for one person or small team on cloud cluster
- Mesos - This is more useful when you have team of developers using same spark clusters
- Yarn - This is more useful when you have team of developers using same spark clusters



An example of set-up used in these lessons
- Data Storage (on S3)
- Multiple EC2 machines created to build spark cluster

### Need to attach EC2 vs EMR comparision picture here

Circling back about HDFS
Previously we have looked over the Hadoop Ecosystem. To refresh those concepts, we have provided reference material here. HDFS (Hadoop Distributed File System) is the file system. HDFS uses MapReduce system as a resource manager.

Spark can replace the MapReduce algorithm. Since Spark does not have its own distributed storage system, it leverages using HDFS or AWS S3, or any other distributed storage. Primarily in this course, we will be using AWS S3, but let’s review the advantages of using HDFS over AWS S3.

What is HDFS?
HDFS (Hadoop Distributed File System) is the file system in the Hadoop ecosystem. Hadoop and Spark are two frameworks providing tools for carrying out big-data related tasks. While Spark is faster than Hadoop, Spark has one drawback. It lacks a distributed storage system. In other words, Spark lacks a system to organize, store and process data files.

MapReduce System
HDFS uses MapReduce system as a resource manager to allow the distribution of the files across the hard drives within the cluster. Think of it as the MapReduce System storing the data back on the hard drives after completing all the tasks.

Spark, on the other hand, runs the operations and holds the data in the RAM memory rather than the hard drives used by HDFS. Since Spark lacks a file distribution system to organize, store and process data files, Spark tools are often installed on Hadoop because Spark can then use the Hadoop Distributed File System (HDFS).

Why do you need EMR Cluster?
Since a Spark cluster includes multiple machines, in order to use Spark code on each machine, we would need to download and install Spark and its dependencies. This is a manual process. Elastic Map Reduce is a service offered by AWS that negates the need for you, the user, to go through the manual process of installing Spark and its dependencies for each machine.

Setting up AWS
Please refer to the latest AWS documentation to set up an EMR Cluster. (https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-gs.html#emr-getting-started-plan-and-configure)


AWS CLI enables you to run commands to provision, configure, list, delete resources in the AWS cloud. Before you run any of the aws commands (https://docs.aws.amazon.com/cli/latest/reference/), you need to follow three steps:

Install AWS CLI
Create an IAM user with Administrator permissions
Configure the AWS CLI


### Spark important commands 
- spark.stop() --> used to stop spark session explicitly
- which spark-submit --> give you full path where spark-submit is located
- spark submit --master yarn ./lower_songs.py --> this command is used to submit spark jobs
- spark process will print a tracking URL as well, to see the logs and job status on web browser

Github repo for L3 and L4 code -- (https://github.com/udacity/nd027-c3-data-lakes-with-spark/tree/master/Setting_Spark_Cluster_In_AWS/demo_code)


### Differences between HDFS and AWS S3
Since Spark does not have its own distributed storage system, it leverages using HDFS or AWS S3, or any other distributed storage. Primarily in this course, we will be using AWS S3, but let’s review the advantages of using HDFS over AWS S3.

Although it would make the most sense to use AWS S3 while using other AWS services, it’s important to note the differences between AWS S3 and HDFS.

AWS S3 is an object storage system that stores the data using key value pairs, namely bucket and key, and HDFS is an actual distributed file system which guarantees fault tolerance. HDFS achieves fault tolerance by having duplicate factors, which means it will duplicate the same files at 3 different nodes across the cluster by default (it can be configured to different numbers of duplication).

HDFS has usually been installed in on-premise systems, and traditionally have had engineers on-site to maintain and troubleshoot Hadoop Ecosystem, which cost more than having data on cloud. Due to the flexibility of location and reduced cost of maintenance, cloud solutions have been more popular. With extensive services you can use within AWS, S3 has been a more popular choice than HDFS.

Since AWS S3 is a binary object store, it can store all kinds of format, even images and videos. HDFS will strictly require a certain file format - the popular choices are avro and parquet, which have relatively high compression rate and which makes it useful to store large dataset.


## Need to understand/recall most common HDFS commands

* HDFS does not support "Image files and zip files" *

