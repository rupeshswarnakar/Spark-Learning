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
