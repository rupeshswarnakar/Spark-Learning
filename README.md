# Spark Learning
```
Spark is a distributed processing engine that processes on large dataset parallelly across the cluster of machines.

The speed and performance of Spark is higher than Map/Reduce. It is because spark is in-memory system where memory (RAM) is used to share outputs across the machines.
However, in map/reduce it is not the case. Map/reduce uses Hard disk to share intermediate files across machines, which is slower.

Map/reduce does batch processing which is processing a large, fixed dataset at once.
However, Spark does both batch processing and stream processing where stream processing is processing on data continuously that arrives on real time.

Spark can integrate with any kind of data sources hoever map/reducer are limited with source integration.
