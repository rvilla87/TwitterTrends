# Big-Data

## Table of Contents
|Project |Description |Keywords|
|:----------|:-------------|:--------|
| [ETL with Spark and HDFS](https://github.com/rvilla87/Big-Data#big-data)| ETL (Extract, Transform and Load) with the Spark Python API (PySpark) and Hadoop Distributed File System (HDFS).| *Spark, Spark SQL, PySpark, Hadoop, HDFS, CVS, Apache Parquet* |
| [MongoDB Tutorial and examples](https://github.com/rvilla87/Big-Data#project-2-mongodb-tutorial-and-examples) | Some uses cases of Pymongo (MongoDB with Python) | *MongoDB, Pymongo, documents, Geospatial querys* |


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

Then you can go to [jupyter ETL example](./jupyter/ETL.ipynb) in order to see some ETL with PySpark.



## Project 2: MongoDB Tutorial and examples
[MongoDB.ipynb](./jupyter/MongoDB.ipynb): Some uses cases of Pymongo (**MongoDB** with Python) that includes:
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