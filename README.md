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
* [Maven](#Maven)
    * [What is Maven](#What-is-Maven)
    * [How to install Maven](#How-to-install-Maven)
* [Spark](#Spark)
    * [What is Spark](#What-is-Spark)
    * [Why Spark](#Why-Spark)
    * [How a Spark Application Runs on a Cluster](#How-a-Spark-Application-Runs-on-a-Cluster)
    * [Spark Mode](#Spark Mode)
* [Hive](#Hive)
    * [What is Hive](#What-is-Hive)
    * [How to install Hive](#How-to-install-Hive)
    * [Get Data from Hive with Spark](#Get-Data-from-Hive-with-Spark)
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

unzip

```
$ tar -zxvf xxx.tar.gz
```

### Step 4 Configure Hadoop

hadoop-env.sh -> Hadoop operating environment

Add Java home path

core-site.xml -> Global parameters

'''
<configuration>
      <property>
            <name>fs.defaultFS</name>
            <value>hdfs://localhost:9000</value> #the URL of namenode
      </property>
      <property>
            <name>hadoop.tmp.dir</name>
            <value>/Users/xiangluo/hadoop2_data/tmp</value>
      </property>
</configuration>
'''

hdfs-site.xml

```
<configuration>
      <property>
         <name>dfs.replication</name>
         <value>1</value>
      </property>
      <property>
         <name>dfs.namenode.name.dir</name> 
         <value>/Users/xiangluo/hadoop2_data/hdfs/namenode</value>
      </property>
      <property>
         <name>dfs.datanode.data.dir</name> 
         <value>/Users/xiangluo//hadoop2_data/hdfs/datanode</value>
      </property>
</configuration>
```
Replication Factor:

It is basically the number of times Hadoop framework replicate each and every Data Block. Block is replicated to provide Fault Tolerance. The default replication factor is 3 which can be configured as per the requirement; it can be changed to 2 (less than 3) or can be increased (more than 3.).

yarn-site.xml

```
<configuration>
<!-- Site specific YARN configuration properties -->
   <property>
      <name>yarn.nodemanager.aux-services</name>
      <value>mapreduce_shuffle</value>
   </property>
   <property>
      <name>yarn.nodemanager.aux-service.mapreduce.shuffle.class</name>
      <value>org.apache.hadoop.mapred.ShuffleHandler</value>
</property>

</configuration>
```

mapred-site.xml

```
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>
```
### Step 5 Initialize Hadoop Cluster

Format the filesystem:

```
$ bin/hdfs namenode -format
```

### Step 6 Start Hadoop Cluster

Start NameNode daemon and DataNode daemon:

Method 1
```
$ sbin/start-dfs.sh
```
Another way:
```
$ sbin/hadoop-daemon.sh start namenode
$ sbin/hadoop-daemon.sh start datanode
```

Browse the web interface for the NameNode; by default it is available at: NameNode - http://localhost:50070/

Start YARN:

```
$ sbin/start-yarn.sh
```
Browse the web interface for the YARM; by default it is available at http://localhost:8088/

Run jps command again to verify all the running processes
```
jps
```

### Step 7 Verify Hadoop Installation

```
$ hadoop fs -mkdir /data
$ hadoop fs -put hadoop-mapreduce-examples-2.7.7.jar /data
$ hadoop jar hadoop-mapreduce-examples-2.7.7.jar pi 2 3

$ hadoop fs -mkdir /data/input
$ hadoop fs -put README.txt /data/input
$ hadoop jar hadoop-mapreduce-examples-2.7.7.jar wordcount /data/input /data/output
$ hadoop fs -cat /data/output/part-r-00000   
```


# Yarn
## What is Yarn

YARN (Yet Another Resource Negotiator) is the resource management layer for the Apache Hadoop ecosystem.

YARN has three components:

Resource Manager: There is exactly one resource manager in one Hadoop Cluster. It does what its name says, managing the resources.

Node Manager: Each data node has one Node Manager. Each Node Manager reports to Resource Manager.

Node Manager=Your Team Lead

Resource Manager=Your Manager

Application Manager: It receives the tasks(known as Applications) that are submitted to the cluster and assigns it to the data nodes

The code(or the Job) from the Client node has to be transferred to the Data node for processing the data. This code is the set of instructions as to what has to be inferred from the data.

This code is first submitted to the AM by the Client Node. The AM requests the RM present in the Name Node for resources to be allotted. The RM in turn contacts the NM in each Data Node that is assigned for this job.

# Maven
## What is Maven

Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information.

## How to install Maven

Maven 3.3+ require JDK 1.7 or above to execute 

### Step 1 Download
### Step 2 Change the path of local repository if necessary

  Default: ${user.home}/.m2/repository
  
  <localRepository>/path/to/local/repo</localRepository>


# Spark
## What is Spark

Apache Spark is an open-source distributed cluster-computing framework. Spark is a data processing engine developed to provide faster and easy-to-use analytics than Hadoop MapReduce. Before Apache Software Foundation took possession of Spark, it was under the control of University of California, Berkeley’s AMP Lab.

## Why Spark

Apache Spark — it’s a lightning-fast cluster computing tool. 

Spark runs applications up to 100x faster in memory and 10x faster on disk than Hadoop by reducing the number of read-write cycles to disk and storing intermediate data in-memory.

Hadoop MapReduce — MapReduce reads and writes from disk, which slows down the processing speed and overall efficiency.

## How a Spark Application Runs on a Cluster
The diagram below shows a Spark application running on a cluster.

A Spark application runs as independent processes, coordinated by the SparkSession object in the driver program.
The resource or cluster manager assigns tasks to workers, one task per partition.
A task applies its unit of work to the dataset in its partition and outputs a new partition dataset. Because iterative algorithms apply operations repeatedly to data, they benefit from caching datasets across iterations.
Results are sent back to the driver application or can be saved to disk.


## Spark Mode

Spark supports the following resource/cluster managers:

Spark Standalone – a simple cluster manager included with Spark(If there are multiple machines, then Spark should be deployed on each machine)

Apache Mesos – a general cluster manager that can also run Hadoop applications

Apache Hadoop YARN – the resource manager in Hadoop 2. The Spark job is submitted to Hadoop(YARN) to run and Spark is only a client here.

Kubernetes – an open source system for automating deployment, scaling, and management of containerized applications

Local mode, where the driver and executors run as threads on your computer instead of a cluster, which is useful for developing your applications from a personal computer.



# Hive
# What is Hive

Apache Hive is an open source data warehouse software for reading, writing and managing large data set files that are stored directly in either the Apache Hadoop Distributed File System (HDFS) or other data storage systems such as Apache HBase. Hive enables SQL developers to write Hive Query Language (HQL) statements that are similar to standard SQL statements for data query and analysis.  It is designed to make MapReduce programming easier because you don’t have to know and write lengthy Java code. Instead, you can write queries more simply in HQL, and Hive can then create the map and reduce the functions.

# How to install Hive

## Step 1 Install Mysql

## Step 2 Download JDBC driver

Platform independent (v8.0.19 is used here)

Copy the JDBC driver to hive lib folder

## Step 3 Configurate Hive

```
$ cp hive-default.xml.template hive-site.xml
```

Make some changes in hive-site.xml
```
<property>
  <name>javax.jdo.option.ConnectionURL</name>
  <value>jdbc:mysql://localhost/metastore?serverTimezone=PST</value>
</property>
<property>
  <name>javax.jdo.option.ConnectionDriverName</name>
  <value>com.mysql.cj.jdbc.Driver</value>
</property>
<property>
  <name>javax.jdo.option.ConnectionUserName</name>
  <value>hiveuser</value>
</property>
<property>
  <name>javax.jdo.option.ConnectionPassword</name>
  <value>12345678</value>
</property>
<property>
    <name>hive.exec.local.scratchdir</name>
    <value>/Users/xiangluo/hadoop2_data/hive</value>
    <description>Local scratch space for Hive jobs</description>
</property>
<property>
    <name>hive.downloaded.resources.dir</name>
    <value>/Users/xiangluo/hadoop2_data/hive</value>
    <description>Temporary local directory for added resources in the remote file system.</description>
</property>
<property>
    <name>hive.querylog.location</name>
    <value>/Users/xiangluo/hadoop2_data/hive<value>
    <description>Location of Hive run time structured log file</description>
</property>
```

start My sql with below command:
```
$ mysql -uroot -p12345678

$ mysql
mysql> CREATE DATABASE metastore;
mysql> USE metastore;
mysql> CREATE USER 'hiveuser'@'localhost' IDENTIFIED BY 'password';
mysql> GRANT SELECT,INSERT,UPDATE,DELETE,ALTER,CREATE, REFERENCES, INDEX ON metastore.* TO 'hiveuser'@'localhost';
```

run the schematool so that hive will use mysql
```
./schematool -initSchema -dbType mysql 
```

## Step 4 Start Hive

```
$hive
hive > show tables;
```

## Step 5 Verify Hive Installation

```
hive> show databases;
OK
default
Time taken: 3.516 seconds, Fetched: 1 row(s)
hive> use default;
OK
Time taken: 0.024 seconds
hive> show tables;
OK
Time taken: 0.044 seconds
hive> create table pk(id int, name string) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t';
OK
Time taken: 0.785 seconds
hive> show tables;
OK
pk
Time taken: 0.037 seconds, Fetched: 1 row(s)
hive> select * from pk;
OK
Time taken: 1.104 seconds
hive> load data local inpath '/Users/xiangluo/data/names.txt' overwrite into table default.pk;
Loading data to table default.pk
OK
Time taken: 0.714 seconds
hive> select * from pk;
OK
1	zhangsan
2	lisi
3	Louis
Time taken: 0.102 seconds, Fetched: 3 row(s)
hive> select count(*) from pk;
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = xiangluo_20200506042554_a0d8a976-8101-4c72-92bc-cec6b3ba180f
Total jobs = 1
Launching Job 1 out of 1
Number of reduce tasks determined at compile time: 1
In order to change the average load for a reducer (in bytes):
  set hive.exec.reducers.bytes.per.reducer=<number>
In order to limit the maximum number of reducers:
  set hive.exec.reducers.max=<number>
In order to set a constant number of reducers:
  set mapreduce.job.reduces=<number>
Starting Job = job_1588757981006_0003, Tracking URL = http://localhost:8088/proxy/application_1588757981006_0003/
Kill Command = /Users/xiangluo/app/hadoop-2.7.7/bin/hadoop job  -kill job_1588757981006_0003
Hadoop job information for Stage-1: number of mappers: 1; number of reducers: 1
2020-05-06 04:26:01,181 Stage-1 map = 0%,  reduce = 0%
2020-05-06 04:26:06,377 Stage-1 map = 100%,  reduce = 0%
2020-05-06 04:26:11,533 Stage-1 map = 100%,  reduce = 100%
Ended Job = job_1588757981006_0003
MapReduce Jobs Launched: 
Stage-Stage-1: Map: 1  Reduce: 1   HDFS Read: 7588 HDFS Write: 101 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
3
Time taken: 17.969 seconds, Fetched: 1 row(s)
hive> 
```

Metastore is the central repository of Apache Hive metadata. It stores metadata for Hive tables (like their schema and location) and partitions in a relational database. It provides client access to this information by using metastore service API.

# Get Data from Hive with Spark

```
$ cp $HIVE_HOME/conf/hive-site.xml $SPARK_HOME/conf/
$ spark-shell --master local --jars ~/app/mysql-connector-java-8.0.19.jar 
$ spark.sql("show tables").show
$ spark.sql("select * from pk").show
```
But
```
$ spark-sql --master local --jars ~/app/mysql-connector-java-8.0.19.jar
```

Error will occur

```
No suitable driver found for jdbc:mysql://localhost/metastore?serverTimezone=PST
```

```
$ spark-sql --master local --jars ~/app/mysql-connector-java-8.0.19.jar --driver-class-path ~/app/mysql-connector-java-8.0.19.jar
```

Another method

Copy mysql jar package to $SPARK_HOME/jars, then for any Spark application, the mysql jar package will be loaded

```
spark-sql> select * from pk;
```

Start thriftserver
```
$ ./sbin/start-thriftserver.sh --master local --jars ~/app/mysql-connector-java-8.0.19.jar 
$ tail -200f /Users/xiangluo/app/spark-2.4.5-bin-hadoop2.7/logs/spark-xiangluo-org.apache.spark.sql.hive.thriftserver.HiveThriftServer2-1-Xiangs-MacBook-Pro.local.out
```


Error may occur
```
org.apache.thrift.transport.TTransportException: Could not create ServerSocket on address 0.0.0.0/0.0.0.0:10000.
	at org.apache.thrift.transport.TServerSocket.<init>(TServerSocket.java:109)
	at org.apache.thrift.transport.TServerSocket.<init>(TServerSocket.java:91)
	at org.apache.thrift.transport.TServerSocket.<init>(TServerSocket.java:87)
	at org.apache.hive.service.auth.HiveAuthFactory.getServerSocket(HiveAuthFactory.java:275)
	at org.apache.hive.service.cli.thrift.ThriftBinaryCLIService.run(ThriftBinaryCLIService.java:66)
	at java.lang.Thread.run(Thread.java:748)
Caused by: java.net.BindException: Address already in use (Bind failed)
	at java.net.PlainSocketImpl.socketBind(Native Method)
	at java.net.AbstractPlainSocketImpl.bind(AbstractPlainSocketImpl.java:387)
	at java.net.ServerSocket.bind(ServerSocket.java:375)
	at org.apache.thrift.transport.TServerSocket.<init>(TServerSocket.java:106)
```

Showing that the 10000 port is being used.
```
$ lsof -i:8080, to list the process (pid) running on port 8080.Then kill the process with kill <pid>
```


```
$ jps
$ ps -ef|grep 92436
```

start beeline
```
beeline -u jdbc:hive2://localhost:10000
```

```
0: jdbc:hive2://localhost:10000> select * from pk;
```

We can also start another beeline client
```
beeline -u jdbc:hive2://localhost:10000
```

Multiple beeline clients can run on thriftserver


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
