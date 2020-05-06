# Big_Data_Tools_Installation_And_Configuration
The description of big data tools installation and configuration


---
Table of Contents

* [Hadoop](#Hadoop)
    * [What is Hadoop](#What-is-Hadoop)
    * [What is MapReduce](#What-is-MapReduce)
    * [What is HDFS](#What-is-HDFS)
    * [Namenode and Datanode](#Namenode-and-Datanode)
    * [Different Hadoop Modes](#Different-Hadoop-Modes)
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

MapReduce Process

Input Splits:

An input to a MapReduce job is divided into fixed-size pieces called input splits Input split is a chunk of the input that is consumed by a single map

Mapping

This is the very first phase in the execution of map-reduce program. In this phase data in each split is passed to a mapping function to produce output values. In our example, a job of mapping phase is to count a number of occurrences of each word from input splits (more details about input-split is given below) and prepare a list in the form of <word, frequency>

Shuffling

This phase consumes the output of Mapping phase. Its task is to consolidate the relevant records from Mapping phase output. In our example, the same words are clubed together along with their respective frequency.

Reducing

In this phase, output values from the Shuffling phase are aggregated. This phase combines values from Shuffling phase and returns a single output value. In short, this phase summarizes the complete dataset.


## What is HDFS

HDFS is the primary data storage system used by Hadoop applications. HDFS is a block structured distributed filesystem that is designed to store petabytes of data reliably on compute clusters made out of commodity hardware. HDFS overlays on top of the existing filesystem of the compute nodes and stores files by breaking them into coarser grained blocks (for example, 128 MB).

HDFS is highly fault-tolerant and is designed to be deployed on low-cost hardware. HDFS provides high throughput access to application data and is suitable for applications that have large data sets. HDFS relaxes a few POSIX requirements to enable streaming access to file system data.

## Namenode and Datanode

HDFS has a master/slave architecture. An HDFS cluster consists of a single NameNode, a master server that manages the file system namespace and regulates access to files by clients. In addition, there are a number of DataNodes, usually one per node in the cluster, which manage storage attached to the nodes that they run on. HDFS exposes a file system namespace and allows user data to be stored in files. Internally, a file is split into one or more blocks and these blocks are stored in a set of DataNodes. The NameNode executes file system namespace operations like opening, closing, and renaming files and directories. It also determines the mapping of blocks to DataNodes. The DataNodes are responsible for serving read and write requests from the file system’s clients. The DataNodes also perform block creation, deletion, and replication upon instruction from the NameNode.

## Different Hadoop Modes

1. Local Mode or Standalone Mode

Standalone mode is the default mode in which Hadoop run. Standalone mode is mainly used for debugging where you don’t really use HDFS.

You can use input and output both as a local file system in standalone mode.

You also don’t need to do any custom configuration in the files- mapred-site.xml, core-site.xml, hdfs-site.xml.

Standalone mode is usually the fastest Hadoop modes as it uses the local file system for all the input and output. Here is the summarized view of the standalone mode

• Used for debugging purpose

• HDFS is not being used

• Uses local file system for input and output

• No need to change any configuration files

• Default Hadoop Modes

2. Pseudo-distributed Mode

The pseudo-distribute mode is also known as a single-node cluster where both NameNode and DataNode will reside on the same machine.

In pseudo-distributed mode, all the Hadoop daemons will be running on a single node. Such configuration is mainly used while testing when we don’t need to think about the resources and other users sharing the resource.

In this architecture, a separate JVM is spawned for every Hadoop components as they could communicate across network sockets, effectively producing a fully functioning and optimized mini-cluster on a single host.

Here is the summarized view of pseudo distributed Mode

• Single Node Hadoop deployment running on Hadoop is considered as pseudo distributed mode

• All the master & slave daemons will be running on the same node

• Mainly used for testing purpose

• Replication Factor will be ONE for blocks

• Changes in configuration files will be required for all the three files- mapred-site.xml, core-site.xml, hdfs-site.xml

3. Fully-Distributed Mode (Multi-Node Cluster)

This is the production mode of Hadoop where multiple nodes will be running. Here data will be distributed across several nodes and processing will be done on each node.

Master and Slave services will be running on the separate nodes in fully-distributed Hadoop Mode.

• Production phase of Hadoop

• Separate nodes for master and slave daemons

• Data are used and distributed across multiple nodes

In the Hadoop development, each Hadoop Modes have its own benefits and drawbacks. Definitely fully distributed mode is the one for which Hadoop is mainly known for but again there is no point in engaging the resource while in testing or debugging phase. So standalone and pseudo-distributed Hadoop modes are also having their own significance.


## How to install Hadoop

Pseudo-distributed Mode on Mac OS

Version 2.7 and later of Apache Hadoop requires Java 7 or higher.

### Step 1 Install Java

### Step 2 Configure SSH

The SSH protocol (also referred to as Secure Shell) is a method for secure remote login from one computer to another. It provides several alternative options for strong authentication, and it protects the communications security and integrity with strong encryption.

If you cannot ssh to localhost without a passphrase, execute the following commands:

```
  $ ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
  $ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
  $ chmod 0600 ~/.ssh/authorized_keys
```

### Step 3 Install Hadoop

### Step 4 Configure Hadoop


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
