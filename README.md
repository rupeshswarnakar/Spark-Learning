# Spark Learning

## Why Spark over map/reduce?
```
Spark is a distributed processing engine that processes on large dataset parallelly across the cluster of machines.

The speed and performance of Spark is higher than Map/Reduce. It is because spark is in-memory system where memory (RAM) is used to share outputs across the machines.
However, in map/reduce it is not the case. Map/reduce uses Hard disk to share intermediate files across machines, which is slower.

Map/reduce does batch processing which is processing a large, fixed dataset at once.
However, Spark does both batch processing and stream processing where stream processing is processing on data continuously that arrives on real time.

Spark can integrate with any kind of data sources hoever map/reducer are limited with source integration.

In data storage, we call chunks of data stored across multiple machines as data blocks. In data processing, we call the same data blocks as data partitions.
```

## How Spark works?
```
In map/reduce, we can use custom map/reduce jobs to store files.

In Hive, we can use sql query to store files and access them, use filter, group by, aggregation and so on.

However, in Spark (data processing platform) we can simply read files from data sources, and use different in-built functions such as group by, filter sum etc.
```
## Resilient Distributed Dataset (RDD)?
```
For instance,
If we have 1 GB file to store, we can simple have 8 blocks of data (assuming data block size = 128 MB) and have them stored across multiple machines.
Now, we can have 8 partitions each containing records or objects in a distributed data structure which we can as Resilient Distributed Dataset (RDD).

RDD are fault tolerant, because during processing, if we lose some partitions, then we can quickly go a step back and retrieve the partitions. It is possible because
RDD are immutable so every time we are not modifying them but creating a different version of their original structure. This helps retrieve partitions as needed.
```
## Extraction, Transform, Load (ETL)?
```
- Extraction: Read data from different sources such as HDFS, S3, Redshift, local disk etc.
- Transform: Mainly for me with sql background, sql based transformation such as filet, join, union, group by etc.
- Load: RDD write, save etc. to a output source. This output source can be different than extraction source.
```

## RDD vs Dataframe?
```
RDD is immutable distributed data structure with no schema. Schema means without column names, and their data types information.
While, Dataframe is RDD + schema. It is also immutable. This immutable nature preserve the fault tolerant feature of RDD, Dataframe.
```

## Functions in Spark?
```
Two main functions:
a. Transformation
b. Action

Transformation is basically filter, join, union etc. logic for transforming the data.
Action is a command to execute the trnaformation logic.
```

## Eager vs Lazy Evaluation?
```
In Hive, when we execute sql query it run right away. This right-away execution is called Eager evaluation.
In Spark, when we write transformation logic, it won't execute until we call action on it. This delayed execution is called Lazy evaluation.

The benefit of lazy evaluation is that, Spark get time to create execution plan to optimally run the logic that saves time and memory.

For instance,
If we have a sparksql query that says first filter with id<10, then second line query is where department = 'HR' in partitioned table.
Then, after calling action, Spark will create a execution plan where it will run department = 'HR' before id<10 to optimally run the query.  
```





## Q1. What is the difference between map, flatmap?
```
○	These are transformation functions in spark that help us get one output or multiple output per an input. 
○	Map processes each element individually and obtain one output per an input without flattening. 
    For e.g., [“ab”, “cd”] = map(split)  [[“a”,”b”],[“c”,”d”]]
○	Flatmap expands each element individually and obtain more output than the input. It also flattens nested results into one level. 
    For e.g., [“ab”, “cd”] = flatMap(split)  [“a”,”b”,“c”,”d”]
```
## Q2. What is the difference between RDD and DataFrame?
```
○	RDD and DataFrame are distributed collection of data in Spark.
○	RDD is low-level without schema (rows and columns)
○	Dataframe is high level including schema information.
○	Both are immutable hence; different versions are created during processing that also preserves the original data (fault-tolerant).
```
## Q3. How to control the parallelism in spark?
```
○	Parallelism is basically how many tasks are processed parallelly. And this is controlled by how many partitions there are. 
○	To reduce partitions, we perform coalesce function to reduce parallel tasks.
○	Coalesce reduce partitions in each machine so total partitions may still be high number.
○	It is applicable for small file problem.
○	Since it does not perform shuffling across distributed machines, it is faster.
○	To increase or decrease partitions, we perform repartitions and increase or decrease parallel tasks.
○	Repartition is maintained at totality, so the total partition is not different.
○	Since it performs shuffling of data across machines, it is slower.
○	It is mainly used to handle uneven data
```
## Q4. Please explain followings:
```
○	Spark Driver
    It is the main machine that distributes work to all executors. It is the program that runs the main program. It creates the execution plan and splits jobs into stages and tasks.  
○	Execution Mode
    The execution of tasks can be done locally in our laptop (local mode) or across the distributed cluster of machines (cluster mode). This is called execution mode.
○	Spark executor
    It is the process that performs the task according to the instruction provided by driver node and returns the result.
○	Task
    Task is the smallest unit of work assigned to executor in spark. Generally, one partition is equal to one task.
○	Stages
    It is basically the group of tasks that can run together. If the type of transformation does not change from narrow to wide for instance, then tasks can be grouped into a stage. 
○	Worker Node
    This is the actual machine that executes the task assigned by the driver node. It contains executors, CPU and Memory.
```

