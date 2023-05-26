# Spark
<p>
Apache Spark is a unified engine designed for large-scale distributed data processing, on premises in data centers or in the cloud.

Spark provides in-memory storage for intermediate computations, making it much faster than Hadoop MapReduce. It incorporates libraries with composable APIs for machine learning (MLlib), SQL for interactive queries (Spark SQL), stream processing (Structured Streaming) for interacting with real-time data, and graph processing (GraphX).

Spark’s design philosophy centers around four key characteristics:
<ul>
  <li>Speed</li>

  <li>Ease of use</li>

   <li>Modularity</li>

  <li>Extensibility</li>

</ul>  

Let’s take a look at what this means for the framework.

Speed
Spark has pursued the goal of speed in several ways. First, its internal implementation benefits immensely from the hardware industry’s recent huge strides in improving the price and performance of CPUs and memory. Today’s commodity servers come cheap, with hundreds of gigabytes of memory, multiple cores, and the underlying Unix-based operating system taking advantage of efficient multithreading and parallel processing. The framework is optimized to take advantage of all of these factors.

Second, Spark builds its query computations as a directed acyclic graph (DAG); its DAG scheduler and query optimizer construct an efficient computational graph that can usually be decomposed into tasks that are executed in parallel across workers on the cluster. And third, its physical execution engine, Tungsten, uses whole-stage code generation to generate compact code for execution (we will cover SQL optimization and whole-stage code generation in Chapter 3).

With all the intermediate results retained in memory and its limited disk I/O, this gives it a huge performance boost.

Ease of Use
Spark achieves simplicity by providing a fundamental abstraction of a simple logical data structure called a Resilient Distributed Dataset (RDD) upon which all other higher-level structured data abstractions, such as DataFrames and Datasets, are constructed. By providing a set of transformations and actions as operations, Spark offers a simple programming model that you can use to build big data applications in familiar languages.

Modularity
Spark operations can be applied across many types of workloads and expressed in any of the supported programming languages: Scala, Java, Python, SQL, and R. Spark offers unified libraries with well-documented APIs that include the following modules as core components: Spark SQL, Spark Structured Streaming, Spark MLlib, and GraphX, combining all the workloads running under one engine. We’ll take a closer look at all of these in the next section.

You can write a single Spark application that can do it all—no need for distinct engines for disparate workloads, no need to learn separate APIs. With Spark, you get a unified processing engine for your workloads.

Extensibility
Spark focuses on its fast, parallel computation engine rather than on storage. Unlike Apache Hadoop, which included both storage and compute, Spark decouples the two. That means you can use Spark to read data stored in myriad sources—Apache Hadoop, Apache Cassandra, Apache HBase, MongoDB, Apache Hive, RDBMSs, and more—and process it all in memory. Spark’s DataFrameReaders and DataFrameWriters can also be extended to read data from other sources, such as Apache Kafka, Kinesis, Azure Storage, and Amazon S3, into its logical data abstraction, on which it can operate.

The community of Spark developers maintains a list of third-party Spark packages as part of the growing ecosystem (see Figure 1-2). This rich ecosystem of packages includes Spark connectors for a variety of external data sources, performance monitors, and more.
 
  <p>
  
## Technologies Covered

As part of this custom image built by us, we have included the following.
* Hadoop (HDFS, YARN, and Map Reduce)
* Hive
* Spark 2
* Spark 3
* Jupyter based environment
  

## Setup Hadoop and Spark Lab

### Pre-requisites

Here are the pre-requisites to setup the Hadoop and Spark lab.
* Memory: 16 GB RAM
* CPU: At least Quadcore
* If you are using Windows or Mac, make sure to setup Docker Desktop.
* If your system does not meet the requirement, you need to setup environment using AWS Cloud9.
* Even if you have 16 GB RAM and the Quadcore CPU, the system might slow down once we start the docker containers due to the requirements of the resources. You can always use AWS Cloud9 as fallback option.
* In my case, I will be demonstrating using Cloud9.

### Configure Docker Desktop

If you are using Windows or Mac, you need to change the settings to use as much resources as possible.
* Go to Docker Desktop preferences.
* Change memory to 12 GB.
* Change CPUs to the maximum number.
  
 
  
![Spark](https://github.com/andysingal/Spark/blob/main/Screenshot%202023-05-25%20at%204.55.40%20PM.png)
  
# Apache Spark’s Distributed Execution
If you have read this far, you already know that Spark is a distributed data processing engine with its components working collaboratively on a cluster of machines. Before we explore programming with Spark in the following chapters of this book, you need to understand how all the components of Spark’s distributed architecture work together and communicate, and what deployment modes are available.

Let’s start by looking at each of the individual components shown in Figure below and how they fit into the architecture. At a high level in the Spark architecture, a Spark application consists of a driver program that is responsible for orchestrating parallel operations on the Spark cluster. The driver accesses the distributed components in the cluster—the Spark executors and cluster manager—through a SparkSession.  
  
## Spark driver
As the part of the Spark application responsible for instantiating a SparkSession, the Spark driver has multiple roles: it communicates with the cluster manager; it requests resources (CPU, memory, etc.) from the cluster manager for Spark’s executors (JVMs); and it transforms all the Spark operations into DAG computations, schedules them, and distributes their execution as tasks across the Spark executors. Once the resources are allocated, it communicates directly with the executors.  

![ll](https://github.com/andysingal/Spark/blob/main/Screenshot%202023-05-25%20at%205.01.51%20PM.png)    
  
## SparkSession
In Spark 2.0, the SparkSession became a unified conduit to all Spark operations and data. Not only did it subsume previous entry points to Spark like the SparkContext, SQLContext, HiveContext, SparkConf, and StreamingContext, but it also made working with Spark simpler and easier.

Cluster manager:
  
The cluster manager is responsible for managing and allocating resources for the cluster of nodes on which your Spark application runs. Currently, Spark supports four cluster managers: the built-in standalone cluster manager, Apache Hadoop YARN, Apache Mesos, and Kubernetes.

Spark executor: 
  
A Spark executor runs on each worker node in the cluster. The executors communicate with the driver program and are responsible for executing tasks on the workers. In most deployments modes, only a single executor runs per node.
  
![kk](https://github.com/andysingal/Spark/blob/main/Images/Screenshot%202023-05-25%20at%205.29.03%20PM.png)  

Deployment modes:
  
An attractive feature of Spark is its support for myriad deployment modes, enabling Spark to run in different configurations and environments. Because the cluster manager is agnostic to where it runs (as long as it can manage Spark’s executors and fulfill resource requests), Spark can be deployed in some of the most popular environments—such as Apache Hadoop YARN and Kubernetes  

![pw](https://github.com/andysingal/Spark/blob/main/Images/Screenshot%202023-05-25%20at%205.22.23%20PM.png)  
  

![oo](https://github.com/andysingal/Spark/blob/main/Images/Screenshot%202023-05-25%20at%205.13.39%20PM.png)  
## Spark components
![pp](https://github.com/andysingal/Spark/blob/main/Images/Screenshot%202023-05-25%20at%205.16.07%20PM.png)  
  

## Spark Directories
![nn](https://github.com/andysingal/Spark/blob/main/Images/Screenshot%202023-05-25%20at%205.35.20%20PM.png)  
  
#Transformations and Actions
  
![nr](https://github.com/andysingal/Spark/blob/main/Images/Screenshot%202023-05-26%20at%202.49.36%20PM.png)
  
