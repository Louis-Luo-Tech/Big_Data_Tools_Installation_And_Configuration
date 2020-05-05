# Big_Data_Tools_Installation_And_Configuration
The description of big data tools installation and configuration


---
Table of Contents

* [Hadoop](#Hadoop)
    * [What is Hadoop](#What-is-Hadoop)
    * [What is MapReduce](#What-is-MapReduce)
    * [What is HDFS](#What-is-HDFS)
    * [How to install Hadoop](#How-to-install-Hadoop)
* [Yarn](#Yarn)
    * [What is Yarn](#What-is-Yarn)   
* [Spark](#Spark)
    * [What is Spark](#What-is-Spark)
    * [Why Spark](#Why-Spark)
    * [How to install Spark](#How-to-install-Spark)
* [Hive](#Hive)
    * [What is Hive](#What-is-Hive)
* [Hbase](#Hbase)
* [Flume](#Flume)
* [Kafka](#Kafka)
    * [What is Kafka](#What-is-Kafka)
* [Sqoop](#Sqoop)
    * [What is Sqoop](#What-is-Sqoop)
* [Zookeeper](#Zookeeper)


# Hadoop
## What is Hadoop

Hadoop is an open source distributed processing framework that manages data processing and storage for big data applications in scalable clusters of computer servers. It's at the center of an ecosystem of big data technologies that are primarily used to support advanced analytics initiatives, including predictive analytics, data mining and machine learning. Hadoop systems can handle various forms of structured and unstructured data, giving users more flexibility for collecting, processing and analyzing data than relational databases and data warehouses provide.

## What is MapReduce

MapReduce is a programming paradigm that enables massive scalability across hundreds or thousands of servers in a Hadoop cluster. 

Hadoop MapReduce is a software framework for easily writing applications which process vast amounts of data (multi-terabyte data-sets) in-parallel on large clusters (thousands of nodes) of commodity hardware in a reliable, fault-tolerant manner.

A MapReduce job usually splits the input data-set into independent chunks which are processed by the map tasks in a completely parallel manner. The framework sorts the outputs of the maps, which are then input to the reduce tasks. Typically both the input and the output of the job are stored in a file-system. The framework takes care of scheduling tasks, monitoring them and re-executes the failed tasks.

## What is HDFS


## How to install Hadoop

# Yarn
## What is Yarn

# Spark
## What is Spark

Apache Spark is an open-source distributed cluster-computing framework. Spark is a data processing engine developed to provide faster and easy-to-use analytics than Hadoop MapReduce. Before Apache Software Foundation took possession of Spark, it was under the control of University of California, Berkeley’s AMP Lab.

## Why Spark
## How to install Spark

# Hive
# What is Hive

Apache Hive is an open source data warehouse software for reading, writing and managing large data set files that are stored directly in either the Apache Hadoop Distributed File System (HDFS) or other data storage systems such as Apache HBase. Hive enables SQL developers to write Hive Query Language (HQL) statements that are similar to standard SQL statements for data query and analysis.  It is designed to make MapReduce programming easier because you don’t have to know and write lengthy Java code. Instead, you can write queries more simply in HQL, and Hive can then create the map and reduce the functions.

# Hbase

# Flume

# Flink

# Kafka
# What is Kafka

Apache Kafka is a community distributed event streaming platform capable of handling trillions of events a day. Initially conceived as a messaging queue, Kafka is based on an abstraction of a distributed commit log

Kafka is a distributed streaming platform that is used publish and subscribe to streams of records

publish-subscribe messaging systems

# Sqoop
# What is Sqoop

Sqoop is a tool designed to transfer data between Hadoop and relational database servers. It is used to import data from relational databases such as MySQL, Oracle to Hadoop HDFS, and export from Hadoop file system to relational databases. This is a brief tutorial that explains how to make use of Sqoop in Hadoop ecosystem.


# Zookeeper
