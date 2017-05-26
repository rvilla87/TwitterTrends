# Big-Data

## Project 1: ETL with PySpark+Hadoop (Work in progress)

### Hadoop
Hadoop can be downloaded from [Hadoop releases webpage](http://hadoop.apache.org/releases.html). These releases do not include [winutils](https://github.com/steveloughran/winutils/releases) (Windows binaries for Hadoop versions) required in order to run Hadoop in Windows systems.

#### Configuring Hadoop
Read this guide in order to install Hadoop on Windows: https://wiki.apache.org/hadoop/Hadoop2OnWindows
- *NOTE*: Hadoop requires Java. JDK 8 64bits worked for me.

Windows environment variables:
~~~
JAVA_HOME=C:\Progra~1\Java\jdk1.8.0_131
HADOOP_HOME=C:\hadoop
SPARK_HOME=C:\spark
PYTHONPATH=%SPARK_HOME%\python;
PATH=C:\Python;C:\Python\Scripts;%HADOOP_HOME%\bin;%SPARK_HOME%\bin;%PYTHONPATH%;%PATH%;
~~~

- *NOTES*:
    - JAVA_HOME must match your Java downloaded version (in my case 1.8.0_131). "Progra~1" for 32bits path installation and "Progra~2" for 64bits.
    - PYTHONPATH is the path were Python will look for additional libraries. In this case, is set to look for the spark ones.
    - In path variable %PATH% means the same PATH value you already have. Basically add the new paths at the beginning of the PATH value.
    - In order to avoid troubles, you sould set **hadoop.tmp.dir** in file *\hadoop\etc\hadoop\core-site.xml* with Hadoop tmp directory we want (note that drive letter la unidad is preceded by /). For example:
~~~
  <property>
    <name>hadoop.tmp.dir</name>
    <value>/C:/hadoop/temp/</value>
  </property>
~~~

### PySpark
In order to run need to install the library py4j:
~~~
pip install py4j
~~~

Then you can go to [jupyter ETL example](./PySpark/jupyter/ETL.ipynb) in order to see some ETL with PySpark.