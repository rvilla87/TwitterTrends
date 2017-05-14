# Big-Data

## Project 1: ETL with PySpark+Hadoop (Work in progress)

### Hadoop
Hadoop can be downloaded from http://hadoop.apache.org/releases.html but as the releases do not include Windows binaries we can downloaded from here:

#### Configuring Hadoop
Read this guide in order to install Hadoop on Windows: https://wiki.apache.org/hadoop/Hadoop2OnWindows
- *NOTE*: Hadoop requires Java. JDK 8 64bits worked for me.

- Windows variables:
~~~
%HADOOP_HOME%\etc\hadoop\hadoop-env.cmd
%HADOOP_PREFIX%\sbin\start-dfs.cmd
%HADOOP_PREFIX%\bin\hdfs dfs -put LICENSE.txt /
%HADOOP_PREFIX%\bin\hdfs dfs -ls /
~~~


### PySpark

