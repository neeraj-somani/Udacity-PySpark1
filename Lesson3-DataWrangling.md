## Notes from Lesson 3 - Data Wrangling

## Lesson Overview
- Wrangling data with Spark
- Functional programming
- Read in and write out data
- Spark environment and Spark APIs
- RDD API


## Spark is based on Functional Programming
## Basic Python - is procedural programming style

Why spark uses functional programming?
Because, in the distributred system environment your program can get affteced by the mistake some other system is making.
Funcation programming can control the effect of these mistakes. How?
Because, every system process there own chunk of tasks and each task is independent of each other.

The PySpark API allows you to write programs in Spark and ensures that your code uses functional programming practices. Underneath the hood, the Python code uses py4j to make calls to the Java Virtual Machine (JVM).

Spark uses a concept called Pure function to solve problem of procedural programming.

### Spark DAG and Lazy evaluation concept 
- Spark copies the original data before processing it to create DAG.
- Immutible - also a term used for same concept.
- Every spark programm has many functions, one under the other for various subtasks.
    - if spark has to create a copy of data for these each functions than it requires a lot of memory.
    - Hence, spark uses, Lazy evaluation concept,
        - In this concept, spark creates a copy of your original data (using map concept, key-value pair) and pass it through the entire process to make DAG.
        - In this concept, spark build a detailed instructions about what data is needed at which step.
        - This is same as receipe.
        - Hence, this entire process or concept is known as Directed Acyclic Graph (DAG).

- Once, A DAG is created, spark takes the data at the last moment.
- Stages - This is nothing but building different set of instructions (Lazy Evaluations) in different stages and combine them together to make DAG at the end.


## Lets understand same using code:
- sc.parallelize - command distributes your data to different nodes on your cluster
- data.collect() - command collects the details of Lazy evaluation from all nodes of cluster back to the master node. At the master node level, spark decide about the stages in which it wants to process this data. Meaning, spark build stages and process them as per the details collected by DAG.

### How spark Distribute Data?
- Using HDFS techniques - divide data into blocks of size (64 or 128 MB). This block size can be customized.
- Then these data blocks send across different nodes of clusters.
- These blocks can be stored in multiple locations to make is fault taulerant.

### A spark program consist of below components
- SparkSession - the spark SQL context, this will create spark Data frame
- SparkContext - entry point for spark functionality and connect cluster with application
- sparkConf - Used to configure basic environment settings, like ip-address, block size, etc,

Tips - 
- If Spark is used in a cluster mode all the worker nodes need to have access to the input data source. If you're trying to import a file saved only on the local disk of the driver node you'll receive an error message.
- Loading the file should work if all the nodes have it saved under the same path.








