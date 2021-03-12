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

### Imperitive vs Declarative Programming
- Imperitive - Spark DF and Python
    - it cares about How?
    - In this we are more focused (or specific) on each steps of achiving the result.
- Declarative - Using SQL
    - It cares about what?
    - In this we just focus on getting the result. Not the process
    - Thats why most Declarative systems (like Cassandra) was build on top of Imperitive systems.

Functions
In the previous video, we've used a number of functions to manipulate our dataframe. Let's take a look at the different type of functions and their potential pitfalls.

General functions
We have used the following general functions that are quite similar to methods of pandas dataframes:

select(): returns a new DataFrame with the selected columns
filter(): filters rows using the given condition
where(): is just an alias for filter()
groupBy(): groups the DataFrame using the specified columns, so we can run aggregation on them
sort(): returns a new DataFrame sorted by the specified column(s). By default the second parameter 'ascending' is True.
dropDuplicates(): returns a new DataFrame with unique rows based on all or just a subset of columns
withColumn(): returns a new DataFrame by adding a column or replacing the existing column that has the same name. The first parameter is the name of the new column, the second is an expression of how to compute it.
Aggregate functions
Spark SQL provides built-in methods for the most common aggregations such as count(), countDistinct(), avg(), max(), min(), etc. in the pyspark.sql.functions module. These methods are not the same as the built-in methods in the Python Standard Library, where we can find min() for example as well, hence you need to be careful not to use them interchangeably.

In many cases, there are multiple ways to express the same aggregations. For example, if we would like to compute one type of aggregate for one or more columns of the DataFrame we can just simply chain the aggregate method after a groupBy(). If we would like to use different functions on different columns, agg()comes in handy. For example agg({"salary": "avg", "age": "max"}) computes the average salary and maximum age.

User defined functions (UDF)
In Spark SQL we can define our own functions with the udf method from the pyspark.sql.functions module. The default type of the returned variable for UDFs is string. If we would like to return an other type we need to explicitly do so by using the different types from the pyspark.sql.types module.

Window functions
Window functions are a way of combining the values of ranges of rows in a DataFrame. When defining the window we can choose how to sort and group (with the partitionBy method) the rows and how wide of a window we'd like to use (described by rangeBetween or rowsBetween).

For further information see the Spark SQL, DataFrames and Datasets Guide (https://spark.apache.org/docs/latest/sql-programming-guide.html) and the Spark Python API Docs (https://spark.apache.org/docs/latest/api/python/index.html).








