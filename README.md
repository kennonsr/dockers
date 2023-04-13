# HADOOP Ecosystem Playground Dockers
 
 ## hadoop_hbase_hive_spark_docker
 
**UPDATE** : To have a lighter platform including HBASE service this repo will deploy only Hadoop, Hbase, Zookeeper, Hive, Hive Metastore (PostGresSQL) and Spark. It is possible to add the other services back, together with Hbase, modifying the script files for build and cluster. 

## Services

* [Hadoop 3.3.1](http://hadoop.apache.org/docs/r3.3.1/) HDFS in  Distributed (Multi-node) Mode
* [Hive 2.3.9](http://hive.apache.org/) with HiveServer2
* [Spark 3.1.2](https://spark.apache.org/docs/3.1.2/) in SPARK MASTER mode (Spark Scala, and PySpark) - You can trigger a job also as YARN giving more resources (CPU, MEMORY)
* [Hbase 2.4.15](https://hbase.apache.org/)  in Pseudo Distributed Mode on top of HDFS

Also there is available an EDGE node to run code/scripts

> If you have more resources to run the containers, you can run Spark over YARN, as Defalut, Spark is running with Spark Master (1 Master, 3 workers)

**PS** -> HBASE was added in the platform. Nifi, Hue and Zeppelin were disabled to consume less resources.

**PS2** : Spark and Hadoop are in the version 3 now. for a next step, it will be recreated this Hadoop Ecosystem platform using docker compose (https://docs.docker.com/compose/). The way of this current version is composing throgh scripts.

**UPDATE** : To have a lighter platform including HBASE service this repo will deploy only Hadoop, Hbase, Zookeeper, Hive, Hive Metastore (PostGresSQL) and Spark only. It is possible to add the other services back, together with Hbase, modifying the script files for build and cluster.