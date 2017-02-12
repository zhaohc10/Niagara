<pre>
 ____  _____   _
|_   \|_   _| (_)
  |   \ | |   __   ,--.   .--./) ,--.   _ .--.  ,--.
  | |\ \| |  [  | `'_\ : / /'`\;`'_\ : [ `/'`\]`'_\ :
 _| |_\   |_  | | // | |,\ \._//// | |, | |    // | |,
|_____|\____|[___]\'-;__/.',__` \'-;__/[___]   \'-;__/
                        ( ( __))
</pre>

Niagara is a open-source DaaS platform written in Scala built on top of SMACK(Spark, Mesos, Akka, Cassandra and Kafka) stack.
It is a MVP to evaluate real-time processing frameworks, e.g. Spark Streaming, Akka Stream, Kafka Streams, etc.

# Modules

* Batch Processing

* Real-time Processing

* Data-as-a-Service

## Batch Processing

The batch layer streams the xml files by Spark textfile API.
It parses the xml file line by line into a DataSet.
Queries the dataset by either Dataset API or Spark SQL.
Finally, persists the dataset on HDFS in Parquet format.

### Tech Stack

* Data Formats: XML, Parquet

* Storage Systems: HDFS

* Frameworks: Spark Core/SQL

## Real-time Processing

The real-time layer utilizes Akka Streams to simulate an infinite streaming producer.
Akka streams in the Xml files and emits Avro messages to Kafka simultaneously.
The consumers are implemented by Spark streaming and Kafka Streams. Both of them consume Avro messages from Kafka,
then executes the real-time data analytics.
The ingested data are persisted in Cassandra.

### Tech Stack

* Data Formats: XML, Avro

* Storage Systems: HDFS, Cassandra

* Messaging Systems: Kafka

* Frameworks: Akka Streams, Kafka Streams Spark Streaming/SQL,

## Data-as-a-Service

The service layer provides RESTful APIs built by Akka-Http for users to easily interact with data for ad-hoc analytics.
Under the hood, the service calls Cassandra APIs to implement CRUD operations.

### Tech Stack

* Data Formats: Json

* Storage Systems: Cassandra, MySQL

* Frameworks: Akka-Http, Slick


## Dataset used in the project:

Stack Exchange Dataset contains 28 million posts in a 40GB single XML file.
https://archive.org/details/stackexchange