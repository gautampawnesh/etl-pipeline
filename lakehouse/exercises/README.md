## Outline
1. Big Data Ecosystem
2. Spark Essentials
	How Spark Works
	Wrangling 
	Spark SQL
3. USing Spark in AWS
	AWS Glue
	Data Lakes
	Spark Jobs
4. Ingesting and Organizing Data in Lakehouse:
	PII and Data Privacy
	Streaming Data
	Curated Data

## Refernce :
Github Repository: https://github.com/udacity/nd027-Data-Engineering-Data-Lakes-AWS-Exercises

## Project Overview

The Challenge
In this project you'll act as a data engineer for the STEDI team to build a Data Lakehouse solution for sensor data that trains a machine learning model. The STEDI team has been hard at work developing a hardware STEDI step trainer that trains the user to do a balance exercise.

The Device
There are sensors on the device that collect data to train a machine learning algorithm to detect steps. It also has a companion mobile app that collects customer data and interacts with the device sensors. The step trainer is just a motion sensor that records the distance of the object detected.

The Project
At the end of the course you'll work on a project to build data pipelines that use Apache Spark to store, filter, process, and transform data from STEDI users for data analytics and machine learning applications.


## Intro to Big Data Ecosystem, Spark and Data Lakes
The modern big data ecosystem is an evolution of data processing on distributed architecture necessary to handle the sheer volume of data.

As businesses began gathering and processing ever larger amounts of data, the field of data science arose around the need to thoughtfully ask questions of data and answer them using scientific methods of discovery. In addition, ever-increasing amounts of data along with greater processing power led to a surge in artificial intelligence research.

Data Science and AI are immensely important to the modern business but without a big data ecosystem to move, store, clean, merge, and tidy up data, these tools are not effective. This is why the work of a data engineer is so critical. It is you, the data engineer, who will skillfully use modern tools and techniques to create the big data ecosystem.

![Ecosystem](./docs/ecosystem.png)

Early efforts at processing large amounts of structured, semi-structured, and unstructured data led to the development of Hadoop. Hadoop incorporates two key components:

The Hadoop Distributed File System (or HDFS) provides distributed storage with high-throughput access to data.
MapReduce provides a way to conduct massive parallel processing for large amounts of data.
The next step in the evolution was Apache Spark.

Spark built on the ideas of Hadoop and provided multiple programming APIs for processing data as well as providing an interactive interface for iteratively developing data engineering and data science solutions.

Hadoop and Spark have led to the development and popularity of data lakes to process large amounts of both structured and unstructured data.

Finally, the latest step in the evolution of big data ecosystems is the lake house architecture. Lake house seeks to combine the strengths of both data lakes and data warehouses.

![HadoopToDataLakes](./docs/hadoopToDL.png)

Data warehouses are based on specific and explicit data structures that allow for highly performant business intelligence and analytics but they do not perform well with unstructured data.

Data lakes are capable of ingesting massive amounts of both structured and unstructured data with Hadoop and Spark providing processing on top of these datasets.

Data lakes have several shortcomings that grew out of their flexibility. They are unable to support transactions and perform poorly with changing datasets. Data governance became difficult due to the unstructured nature of these systems.

Modern lakehouse architectures seek to combine the strengths of data warehouses and data lakes into a single, powerful architecture.


### Hadoop Vocabulary
Here is a list of some terms associated with Hadoop. You'll learn more about these terms and how they relate to Spark in the rest of the lesson.

Hadoop(opens in a new tab) - an ecosystem of tools for big data storage and data analysis. Hadoop is an older system than Spark but is still used by many companies. The major difference between Spark and Hadoop is how they use memory. Hadoop writes intermediate results to disk whereas Spark tries to keep data in memory whenever possible. This makes Spark faster for many use cases.

Hadoop MapReduce - a system for processing and analyzing large data sets in parallel.

Hadoop YARN - a resource manager that schedules jobs across a cluster. The manager keeps track of what computer resources are available and then assigns those resources to specific tasks.

Hadoop Distributed File System (HDFS) - a big data storage system that splits data into chunks and stores the chunks across a cluster of computers.

As Hadoop matured, other tools were developed to make Hadoop easier to work with. These tools included:

Apache Pig - a SQL-like language that runs on top of Hadoop MapReduce
Apache Hive - another SQL-like interface that runs on top of Hadoop MapReduce
Oftentimes when someone is talking about Hadoop in general terms, they are actually talking about Hadoop MapReduce. However, Hadoop is more than just MapReduce

## How is Spark related to Hadoop?
Spark, which is the main focus of this course, is another big data framework. Spark contains libraries for data analysis, machine learning, graph analysis, and streaming live data. Spark is generally faster than Hadoop. This is because Hadoop writes intermediate results to disk whereas Spark tries to keep intermediate results in memory whenever possible.

The Hadoop ecosystem includes a distributed file storage system called HDFS (Hadoop Distributed File System). Spark, on the other hand, does not include a file storage system. You can use Spark on top of HDFS but you do not have to. Spark can read in data from other sources as well.

## Streaming Data
Data streaming is a specialized topic in big data. The use case is when you want to store and analyze data in real-time such as Facebook posts or Twitter tweets.

Spark has a streaming library called Spark Streaming[https://spark.apache.org/docs/latest/streaming-programming-guide.html]. Other popular streaming libraries include Storm([http://storm.apache.org/]) and Flink[https://flink.apache.org/]. 

## Map Reduce
MapReduce is a programming technique for manipulating large data sets. "Hadoop MapReduce" is a specific implementation of this programming technique.

The technique works by first dividing up a large dataset and distributing the data across a cluster. In the map step, each data is analyzed and converted into a (key, value) pair. Then these key-value pairs are shuffled across the cluster so that all keys are on the same machine. In the reduce step, the values with the same keys are combined together.

While Spark doesn't implement MapReduce, you can write Spark programs that behave in a similar way to the map-reduce paradigm.

## Why Spark?
Spark is currently one of the most popular tools for big data analytics. Hadoop is a slightly older technology, although still in use by some companies. Spark is generally faster than Hadoop, which is why Spark has become more popular over the last few years.

There are many other big data tools and systems, each with its own use case. For example, there are database system like Apache Cassandra(opens in a new tab) and SQL query engines like Presto(opens in a new tab). But Spark is still one of the most popular tools for analyzing large data sets.

## Spark Cluster
When we talk about distributed computing, we generally refer to a big computational job executing across a cluster of nodes. Each node is responsible for a set of operations on a subset of the data. At the end, we combine these partial results to get the final answer. But how do the nodes know which task to run and demote order? Are all nodes equal? Which machine are you interacting with when you run your code?

Most computational frameworks are organized into a master-worker hierarchy:

1. The master node is responsible for orchestrating the tasks across the cluster
2. Workers are performing the actual computations

There are four different modes to setup Spark:

1. Local mode: In this case, everything happens on a single machine. So, while we use spark's APIs, we don't really do any distributed computing. The local mode can be useful to learn syntax and to prototype your project.
The other three modes are distributed and declare a cluster manager. The cluster manager is a separate process that monitors available resources and makes sure that all machines are responsive during the job. There are three different options of cluster managers:

2. Spark's own Standalone Cluster Manager
In this course, you will set up and use your own distributed Spark cluster using Standalone mode.
In Spark's Standalone mode there is a Driver Process. If you open a Spark shell, either Python or Scala, you are directly interacting with the driver program. It acts as the master and is responsible for scheduling tasks
3. YARN from the Hadoop project
4. Another open-source manager from UC Berkeley's AMPLab Coordinators.

