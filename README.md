# Udacity-PySpark1

This notebook will cover concepts learned in Udacity pySpark course -- https://classroom.udacity.com/courses/ud2002

Section 2 -
Power of Spark --

1. What is big data?
- When you can't use single machine and requires distributed systems to process your data.
- Mordern Hardware capabilities define 
  - CPU ? - How long does it take your CPU to perform a specific task
     - Brian of computer
     - The CPU can also store small amounts of data inside itself in what are called registers. These registers hold data that the CPU is working with at the moment.
     - The registers make computations more efficient: the registers avoid having to send data unnecessarily back and forth between memory (RAM) and the CPU.
     - 200x times faster than memory
     
  - Memory (RAM) ? - How quickly can you lookup some file that is cache in your systems memory, example "calender that is cached in system"?
      - When your program runs, data gets temporarily stored in memory before getting sent to the CPU. Memory is ephemeral storage - when your computer shuts down, the data in the memory is lost.
      - 15x times faster than SSD
      
  - SSD ? - How many seconds does it take to load data from SSD to app.
      - Cheap but relatively slow compared to cache memory
      - 20x times faster than network
      
  - Network ? - How much data can you download from networks in a min.
      - LAN or Internet - a gateway for other computer tasks
      - Which component is the biggest bottleneck when working with big data?
          - Transfering data across network!
          - Thats why in spark System Design, we use clusters (that conneted by a reliable network), to avoids these network bottleneck issues and even avoid (shuffeling) moving data back and forth between nodes of a cluster. Complete processing of each set of data happend with-in each node of cluster and then merge together before delivering.
          
 
 **That's correct! CPU operations are fastest. Operations in memory (RAM) are the second fastest. Then comes hard disk storage and finally transferring data across a network. Keep these relative speeds in mind. They'll help you understand the constraints when working with big data.**
 
 *Things to understand as well*
 
 - It seems like the right combination of CPU and memory can help you quickly load and process data.
 - Charachtersitics of Memory
    - Efficient
    - Ephemeral (loose data when you turn off)
    - Expensive
 - Beyond the fact that memory is expensive and ephemeral, we'll learn that for most use cases in the industry, memory and CPU aren't the bottleneck. Instead the storage and network.
 
  An interactive version of todays Hardware (https://colin-scott.github.io/personal_website/research/interactive_latency.html)

### notes - A case when you can avoid big-data would be to perform operation after filter and divide the dataset in smaller parts.
- An example, how you can avoid using big-data. This is one way to distinquish between need of big-data vs no big-data.
- you can process the data in chunk.
https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-chunking

### History of Distributed and Parallel Computing
- In distributed computing, each node (computer) has its own memory (RAM) and CPU. And various nodes communicate with each other over the network.
- In parallel computing, RAM (memory) is shared amoung various CPU. One machine connects to multiple CPU.

2. Review of the hardware behind big data
3. Introduction to distributed systems

5. Brief history of Spark and big data

Problem with Map Reduce approach --
- After each processing step, the intermediate results are stored to disk

How spark solves this -
- Spark process data in-memory
- Doesn't need to store intermediate results in-memory
- it can perform multiple map reduce jobs in-memory. While Spark doesn't implement MapReduce, you can write Spark programs that behave in a similar way to the map-reduce paradigm. 
- 

6. Common Spark use cases
7. Other technologies in the big data ecosystem

Below two are even better than spark Streaming library

Apache Storm - Streaming Data
Apache Flink - Streaming Data

### Below content id directly from lecture
Hadoop Vocabulary
Here is a list of some terms associated with Hadoop. You'll learn more about these terms and how they relate to Spark in the rest of the lesson.

Hadoop - an ecosystem of tools for big data storage and data analysis. Hadoop is an older system than Spark but is still used by many companies. The major difference between Spark and Hadoop is how they use memory. Hadoop writes intermediate results to disk whereas Spark tries to keep data in memory whenever possible. This makes Spark faster for many use cases.

Hadoop MapReduce - a system for processing and analyzing large data sets in parallel.

Hadoop YARN - a resource manager that schedules jobs across a cluster. The manager keeps track of what computer resources are available and then assigns those resources to specific tasks.

Hadoop Distributed File System (HDFS) - a big data storage system that splits data into chunks and stores the chunks across a cluster of computers.

As Hadoop matured, other tools were developed to make Hadoop easier to work with. These tools included:

Apache Pig - a SQL-like language that runs on top of Hadoop MapReduce
Apache Hive - another SQL-like interface that runs on top of Hadoop MapReduce
Oftentimes when someone is talking about Hadoop in general terms, they are actually talking about Hadoop MapReduce. However, Hadoop is more than just MapReduce. In the next part of the lesson, you'll learn more about how MapReduce works.

How is Spark related to Hadoop?
Spark, which is the main focus of this course, is another big data framework. Spark contains libraries for data analysis, machine learning, graph analysis, and streaming live data. Spark is generally faster than Hadoop. This is because Hadoop writes intermediate results to disk whereas Spark tries to keep intermediate results in memory whenever possible.

The Hadoop ecosystem includes a distributed file storage system called HDFS (Hadoop Distributed File System). Spark, on the other hand, does not include a file storage system. You can use Spark on top of HDFS but you do not have to. Spark can read in data from other sources as well such as Amazon S3.

Streaming Data
Data streaming is a specialized topic in big data. The use case is when you want to store and analyze data in real-time such as Facebook posts or Twitter tweets.

Spark has a streaming library called Spark Streaming although it is not as popular and fast as some other streaming libraries. Other popular streaming libraries include Storm and Flink. Streaming won't be covered in this course, but you can follow these links to learn more about these technologies.

### How spark Cluster behaves 
- meaning, how each node knows which task they need to perform and what to do after task finished
- In cluster, there is master node, which manages these operations, each child/worker node communicates with master node after completing the tasks.

- Spark Setup modes
  - Local mode
  - cloud or remote machines or could be clusters
      - cluster modes (Standalone, YARN, Mesos)
      - these modes basically makesure than every node in the cluster should be up and running for the task.
      - If at anypoint if cluster has any issues, these modes manages them and inform admin accordingly.

Spark Most Important Use Cases

Spark Use Cases and Resources
Here are a few resources about different Spark use cases:

Data Analytics
Machine Learning
Streaming
Graph Analytics
You Don't Always Need Spark
Spark is meant for big data sets that cannot fit on one computer. But you don't need Spark if you are working on smaller data sets. In the cases of data sets that can fit on your local computer, there are many other options out there you can use to manipulate data such as:

AWK - a command line tool for manipulating text files
R - a programming language and software environment for statistical computing
Python PyData Stack, which includes pandas, Matplotlib, NumPy, and scikit-learn among other libraries
Sometimes, you can still use pandas on a single, local machine even if your data set is only a little bit larger than memory. Pandas can read data in chunks. Depending on your use case, you can filter the data and write out the relevant parts to disk.

If the data is already stored in a relational database such as MySQL or Postgres, you can leverage SQL to extract, filter and aggregate the data. If you would like to leverage pandas and SQL simultaneously, you can use libraries such as SQLAlchemy, which provides an abstraction layer to manipulate SQL tables with generative Python expressions.

The most commonly used Python Machine Learning library is scikit-learn. It has a wide range of algorithms for classification, regression, and clustering, as well as utilities for preprocessing data, fine tuning model parameters and testing their results. However, if you want to use more complex algorithms - like deep learning - you'll need to look further. TensorFlow and PyTorch are currently popular packages.

Spark's Limitations
Spark has some limitation.

Spark Streaming’s latency is at least 500 milliseconds since it operates on micro-batches of records, instead of processing one record at a time. Native streaming tools such as Storm, Apex, or Flink can push down this latency value and might be more suitable for low-latency applications. Flink and Apex can be used for batch computation as well, so if you're already using them for stream processing, there's no need to add Spark to your stack of technologies.

Another limitation of Spark is its selection of machine learning algorithms. Currently, Spark only supports algorithms that scale linearly with the input data size. In general, deep learning is not available either, though there are many projects integrate Spark with Tensorflow and other deep learning tools.

Hadoop versus Spark
The Hadoop ecosystem is a slightly older technology than the Spark ecosystem. In general, Hadoop MapReduce is slower than Spark because Hadoop writes data out to disk during intermediate steps. However, many big companies, such as Facebook and LinkedIn, started using Big Data early and built their infrastructure around the Hadoop ecosystem.

While Spark is great for iterative algorithms, there is not much of a performance boost over Hadoop MapReduce when doing simple counting. Migrating legacy code to Spark, especially on hundreds of nodes that are already in production, might not be worth the cost for the small performance boost.

Beyond Spark for Storing and Processing Big Data
Keep in mind that Spark is not a data storage system, and there are a number of tools besides Spark that can be used to process and analyze large datasets.

Sometimes it makes sense to use the power and simplicity of SQL on big data. For these cases, a new class of databases, know as NoSQL and NewSQL, have been developed.

For example, you might hear about newer database storage systems like HBase or Cassandra. There are also distributed SQL engines like Impala and Presto. Many of these technologies use query syntax that you are likely already familiar with based on your experiences with Python and SQL.

In the lessons ahead, you will learn about Spark specifically, but know that many of the skills you already have with SQL, Python, and soon enough, Spark, will also be useful if you end up needing to learn any of these additional Big Data tools.









Analytical questions for our project (Sparkify) same as Spotify -
- Which artists are played mostly in Canada? Top artists for Canadian Users?
  - Business can decide accordinly to renew artists contract and put terms in contract accordingly
- Analyze log data to understand user activities



 
