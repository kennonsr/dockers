# HADOOP Ecosystem Playground Dockers
 
 ## hadoop_hbase_hive_spark_docker
 
**UPDATE** : To have a lighter platform including HBASE service this repo will deploy only Hadoop, Hbase, Zookeeper, Hive, Hive Metastore (PostGresSQL) Zeppelin and Spark. It is possible to add the other services back, together with Hbase, modifying the script files for build and cluster. 

## Services

* [Hadoop 3.2.0](http://hadoop.apache.org/docs/r3.2.0/) HDFS in  Distributed (Multi-node) Mode
* [Hive 2.3.4](http://hive.apache.org/) with HiveServer2
* [Spark 2.4.0](https://spark.apache.org/docs/2.4.0/) in YARN mode (Spark Scala, and PySpark)
* [Hbase 2.4.15](https://hbase.apache.org/)  in Pseudo Distributed Mode on top of HDFS
* [Zeppelin 0.8.2](https://zeppelin.apache.org/)  Apache Zeppelin - Notebooks

Also there is available an EDGE node to run conde/scripts

**PS** -> HBASE was added in the platform. Nifi and Hue were disabled to consume less resources.
