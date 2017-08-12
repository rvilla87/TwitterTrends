# Big-Data

## Table of Contents
|Project |Description |Keywords|
|:----------|:-------------|:--------|
| [ETL with Spark and HDFS](https://github.com/rvilla87/Big-Data#project-1-etl-with-spark-and-hdfs)| ETL (Extract, Transform and Load) with the Spark Python API (PySpark) and Hadoop Distributed File System (HDFS). [Jupyter Notebook](./jupyter/ETL.ipynb)| *Spark, Spark SQL, PySpark, Hadoop, HDFS, CVS, Apache Parquet* |
| [MongoDB Tutorial and examples](https://github.com/rvilla87/Big-Data#project-2-mongodb-tutorial-and-examples) | Some uses cases of Pymongo (MongoDB with Python).  [Jupyter Notebook](jupyter/MongoDB.ipynb) | *MongoDB, Pymongo, documents, Geospatial querys* |
| [TwitterTrends](https://github.com/rvilla87/Big-Data#project-3-twittertrends) | Get Twitter trends with twitter4j, stream it to a Kafka topic, save it to MongoDB and visualize in Google Maps. Jupyter Notebooks: [1-TrendsToFile](jupyter/TwitterTrends-1-TrendsToFile.ipynb), [2-FileToKafka](jupyter/TwitterTrends-2-FileToKafka.ipynb), [3-KafkaToMongoDB](jupyter/TwitterTrends-3-KafkaToMongoDB.ipynb), [4-MongoDBtoGMaps](jupyter/TwitterTrends-4-MongoDBtoGMaps.ipynb) | *twitter4j, trends, Spark Structured Streaming, dataframe, Kafka, MongoDB, Pymongo, Google Maps, coordinates, ipywidgets*

___

## Project 1: ETL with Spark and HDFS
The goal of this project is to do some ETL (Extract, Transform and Load)  with the Spark Python API ([PySpark](https://spark.apache.org/docs/latest/api/python/pyspark.html)) and Hadoop Distributed File System ([HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsUserGuide.html)).

Working with CSV's files from [HiggsTwitter dataset](http://snap.stanford.edu/data/higgs-twitter.html) we'll do :
- Convert CSV's dataframes to [Apache Parquet](https://parquet.apache.org/) files
- Use **Spark SQL** using DataFrames API and SQL language.
- Some **performance testing** like compressed CSV vs Parquet, cached DF vs not cached DF and local file access vs local HDFS access.

### Preparing the environment
We will need to install/extract Hadoop and Spark, and remember to create the necessary environment variables:

*Windows environment variables (example)*:
~~~
JAVA_HOME=C:\Progra~1\Java\jdk1.8.0_131
HADOOP_HOME=C:\hadoop
SPARK_HOME=C:\spark
PYTHONPATH=%SPARK_HOME%\python;
PATH=C:\Python;C:\Python\Scripts;%HADOOP_HOME%\bin;%SPARK_HOME%\bin;%PYTHONPATH%;%PATH%;
~~~


### Hadoop
Hadoop can be downloaded from [Hadoop releases webpage](http://hadoop.apache.org/releases.html). These releases do not include [winutils](https://github.com/steveloughran/winutils/releases) (Windows binaries for Hadoop versions) required in order to run Hadoop in Windows systems.

#### Configuring Hadoop
Read this guide in order to install Hadoop on Windows: https://wiki.apache.org/hadoop/Hadoop2OnWindows

Some notes to consider:
- Spark and Hadoop and **require Java**. JDK 8 64bits worked for me.
- **JAVA_HOME** must match your Java downloaded version (in my case 1.8.0_131). "Progra\~1" for 32bits path installation and "Progra\~2" for 64bits.
- **PYTHONPATH** is the path were Python will look for additional libraries. In this case, is set to look for the spark ones.
- In **PATH** variable, *%PATH%* means the same PATH value you already have. Basically add the new paths at the beginning of the PATH value.
- In order to avoid troubles, you should set **hadoop.tmp.dir** in file *\hadoop\etc\hadoop\core-site.xml* with Hadoop tmp directory we want (note that drive letter is preceded by /). For example:
~~~
  <property>
    <name>hadoop.tmp.dir</name>
    <value>/C:/hadoop/temp/</value>
  </property>
~~~

### PySpark
In order to run PySpark you need to install the Python library py4j:
~~~
pip install py4j
~~~

Then you can go to [jupyter ETL example](jupyter/ETL.ipynb) in order to see some ETL with PySpark.

___

## Project 2: MongoDB Tutorial and examples
[MongoDB.ipynb](jupyter/MongoDB.ipynb): Some uses cases of Pymongo (**MongoDB** with Python) that includes:
- PyMongo [Tutorial](http://api.mongodb.com/python/current/tutorial.html)
- [Back to Basics](https://www.mongodb.com/presentations/back-to-basics-introduction-to-mongodb)
- [Beyond the Basics](https://www.mongodb.com/presentations/beyond-the-basics-1)
- Inserting, updating, querying, deleting documents.
- Indexing, geospatial indexes
- Geospatial querys:
    - **\$geoWithin**: Selects documents with geospatial data that exists entirely within a specified shape.
    - **\$geoIntersects**: Selects documents whose geospatial data intersects with a specified GeoJSON object.
    - **\$near** and **\$nearSphere**: Specifies a point for which a geospatial query returns the documents from nearest to farthest.
    - **\$geoNear (aggregation)**: Outputs documents in order of nearest to farthest from a specified point. Used to calculate the distance between two points.

___

## Project 3: TwitterTrends
This **streaming project** obtains current **Twitter's trending topic** and show them in **Google Maps** like this:

![twitterTrends](images/twitterTrends.png "twitterTrends")


The project consist in the next 4 processes (each of one is a [Jupyter Notebook](http://jupyter.org/)). Here's a brief description, you can find detailed info inside each notebook:

- **[TwitterTrends-1-TrendsToFile](jupyter/TwitterTrends-1-TrendsToFile.ipynb)** (Scala): It obtains trending topic with twitter4j's methods: [getAvailableTrends](http://twitter4j.org/javadoc/twitter4j/api/TrendsResources.html#getAvailableTrends--) (return locations with trending topics) and [getPlaceTrends](http://twitter4j.org/javadoc/twitter4j/api/TrendsResources.html#getPlaceTrends-int-) (returns the top 10 trending topics for a specific location) and save all info into a file.
- **[TwitterTrends-2-FileToKafka](jupyter/TwitterTrends-2-FileToKafka.ipynb)** (Scala): It streams trending topic from a file to a Kafka topic using Spark Structured Streaming.
- **[TwitterTrends-3-KafkaToMongoDB](jupyter/TwitterTrends-3-KafkaToMongoDB.ipynb)** (Scala): It streams trending topic from a Kafka topic to MongoDB using Spark Structured Streaming.
- **[TwitterTrends-4-MongoDBtoGMaps](jupyter/TwitterTrends-4-MongoDBtoGMaps.ipynb)** (Python): It visualizes trending topic obtained from MongoDB into Google Maps.


### Requirements
- [Oracle JDK 1.8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) (64 bit)
- [Scala 2.11](https://www.scala-lang.org/download/2.11.11.html)
- [Apache Spark 2.2.0](https://spark.apache.org/downloads.html)
- [Apache Kafka 0.11.00 for Scala 2.11](https://www.apache.org/dyn/closer.cgi?path=/kafka/0.11.0.0/kafka_2.11-0.11.0.0.tgz)
- [Generate your own Twitter Tokens](https://dev.twitter.com/oauth/overview/application-owner-access-tokens)
- [Python 3](https://www.python.org/downloads/) and [Gmaps plugin](https://github.com/pbugnion/gmaps) for trending topics visualization. 


### Starting Kafka and MongoDB servers
In order to run [TwitterTrends-2-FileToKafka](jupyter/TwitterTrends-2-FileToKafka.ipynb) we need to start Kafka server. For [TwitterTrends-3-KafkaToMongoDB](jupyter/TwitterTrends-3-KafkaToMongoDB.ipynb) we need to start Kafka server and MongoDB server.

Here's some indications about how to do it:

#### Starting Kafka server
First we need to add Kafka binaries directory in our system PATH and execute the next commands on kafka directory: 

1) Start ZooKeeper instance:
`zookeeper-server-start.bat config/zookeeper.properties`
2) Start the Kafka server
`kafka-server-start.bat config/server.properties`
3) Create a topic (*first run only*):
`kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic tweeterTopic`

You can see detailed explanation as well as the Unix commands in [Kafka Quickstart](https://kafka.apache.org/quickstart).


#### Starting MongoDB server
We need to add MongoDB binaries directory in our system PATH and to type `mongod` in a command line.

Once started, If we want to use a GUI for MongoDB, we can use [MongoDB Compass](https://www.mongodb.com/products/compass).


### Some things to consider
1) [Jupyter Scala](https://github.com/jupyter-scala/jupyter-scala): Scala kernel for Jupyter.

    There's no need to use Jupyter (you can use your favourite Scala development environment) but in order to explain the project in a more interactive way I prefer to use it.
    
    If you plan to use Jupyter Scala you have to take in mind that the way to **manage dependences** (adding external libraries) differs from Jupyter Scala Notebook to a standard Scala IDE/Intellij IDEA with the use of [SBT](http://www.scala-sbt.org/) (Simple Build Tool). For example:
    
    In a standard Scala IDE/Intellij IDEA with the use of SBT we manage libraries adding the next line into our build.sbt file:
    ```Scala
    libraryDependencies += "org.apache.spark" %% "spark-sql" % "2.2.0"
    ```
    
    In Scala Jupyter Notebook we manage libraries executing the next statement in the notebook:	 
    ```Scala
    import $ivy.`org.apache.spark::spark-sql`:2.2.0
    ```

    In either case we need to load the libraries as we normally do, for example: `import org.apache.spark`

___

2) **Spark's logging level**: By default when creating the Spark Session it will show all logging level (even INFO). In order to change this you can set your desired logging level.

    In order to do this you have to copy and rename the *log4j.properties.template* included in your spark/conf folder to spark/conf/log4j.properties and change the following:
    
    `log4j.rootCategory=INFO, console`
    
    to
    
    `log4j.rootCategory=WARN, console`
    
    Now you can import log4j library and set your properties file. For example:
    ``` Scala
    import org.apache.log4j.PropertyConfigurator
    PropertyConfigurator.configure("C:/spark/conf/log4j.properties")
    ```


### Pending tasks
- Implement Structured Streaming from Kafka to MongoDB [when supported](https://jira.mongodb.org/browse/SPARK-85).
- Filter by continent ([\$geoIntersects](https://docs.mongodb.com/manual/reference/operator/query/geoIntersects/#op._S_geoIntersects) with MongoDB).
