# Udacity nanodegree Final Project

This project contains the following:

* consumer_server.py
* data_stream.py
* kafka_server.py
* producer_server.py

#### Q1. How did changing values on the SparkSession property parameters affect the throughput and latency of the data?

Answer:
```python
master("local[*]")
```

This creates Spark in Standalone mode, it can take in a number or * (denoting all available), it controls the number of cores Spark can use on the machine. Large multicore machines can leverage this for parallelism.

#### Q2. What were the 2-3 most efficient SparkSession property key/value pairs? Through testing multiple variations on values, how can you tell these were the most optimal?

Answer:
```python
maxOffsetsPerTrigger
```

This property limits the number of records to fetch per trigger, very large batches affect memmory and smaller batches are an over head in batch creation

```python
maxRatePerPartition
```

The spark.streaming.kafka.maxRatePerPartition configuration is especially crucial to prevent the streaming application from overloading in two scenarios

1. It prevents the first micro-batch from being overwhelmed when there are a large number of unprocessed messages in the Kafka topic initially and we set the auto.offset.reset in Kafka parameters to smallest. 
2. It prevents micro-batches from being overwhelmed when there is a sudden surge of messages from the Kafka producers
