# HADOOP HBASE HIVE SPARK DOCKER CONTAINERS (MacOS and Linux tested)

Thanks to **Aditya Pal** - I forked his original project/repo (https://github.com/sciencepal/dockers) making some changes having a development/lab Hadoop platform for testing purposes. Also with other contributions like Pedro Glongaron (https://github.com/pedro-glongaron) adding more services to master branch of Aditya Pal docker repo.

This project in the original repo has 1 master, 2 workers, 1 edge node (with Flume, Sqoop and Kafka !!) , 1 Hue service node, 1 Zeppelin service node and 1 Nifi node.


**PS** -> HBASE was added in the platform. Nifi, Hue and Zeppelin were disabled to consume less resources.

**PS2** : Spark and Hadoop are in the version 3 now. for a next step, it will be recreated this Hadoop Ecosystem platform using docker compose (https://docs.docker.com/compose/). The way of this current version is composing throgh scripts.

**UPDATE** : To have a lighter platform including HBASE service this repo will deploy only Hadoop, Hbase, Zookeeper, Hive, Hive Metastore (PostGresSQL) and Spark only. It is possible to add the other services back, together with Hbase, modifying the script files for build and cluster.

### This platform was validate with MacOs and Linux, running all the shell scripts. For Windows, using Docker Desktop, it was not totally tested. But the Batch files are present. Also for Windows you can deploy via WSL, but again, you can encounter some issues. Also for windows, before run the build.bat file you must create or add in configs ssh keys id_rsa and id_rsa.pub. You can run via Windows Subsystem for Linux (WSL) ssh-keygen available in the build.sh (bash script).

### Make sure that you build the Dockerfiles for each components in your local environment. Otherwise you will get an older and not tested version from docker hub repo.

## Services

* [Hadoop 3.3.1](http://hadoop.apache.org/docs/r3.3.1/) HDFS in  Distributed (Multi-node) Mode
* [Hive 2.3.9](http://hive.apache.org/) with HiveServer2
* [Spark 3.1.2](https://spark.apache.org/docs/3.1.2/) in SPARK MASTER mode (Spark Scala, and PySpark) - You can trigger a job also as YARN giving more resources (CPU, MEMORY)
* [Hbase 2.4.15](https://hbase.apache.org/)  in Pseudo Distributed Mode on top of HDFS

Also there is available an EDGE node to run conde/scripts

> If you have more resources to run the containers, you can run Spark over YARN, as Defalut, Spark is running with Spark Master (1 Master, 3 workers). Just need to change Spark configuration file.

<br />

**NOTE: Please verify that the download links in the Dockerfiles are still active.**

For Hadoop: Choose any Hadoop version > 2.0 from here https://archive.apache.org/dist/hadoop/core/

For Hive: Choose Hive version > 2.0.0 (preferably < 3.0) from here https://archive.apache.org/dist/hive/

For Spark: Choose Spark version > 2.0 from here https://archive.apache.org/dist/spark/

<br />

**Update: Added pyspark support.**

 ... Change to your default python version in spark Dockerfile

<br />

**Instructions for use**

1. Build cluster using **./build.sh**

2. Once all images are built, install/deploye cluster containers with all configurations by **./cluster.sh Install**

3. Verify the containers running by **docker ps -as**. nodemaster, node2, node3, psqlhms and hbase containers should be running.

4. Enter any container this way: **docker exec -u hadoop -it nodemaster /bin/bash**

5. Once all work is done, bring down cluster by **./cluster.sh stop**

6. Once all containers are created/deployed via install and stopped with the previous command, you can restart cluster keeping the state by **./cluster.sh start**

<br />

**Tests Done with Hive**

1. Copy file from local to nodemaster container : **docker cp test_data.csv nodemaster:/tmp/**

2. Enter nodemaster : **docker exec -u hadoop -it nodemaster /bin/bash**

3. Create directory in HDFS : hadoop@nodemaster:/$ **hdfs dfs -mkdir -p /user/hadoop/test**

4. Get file from container local to HDFS : hadoop@nodemaster:/$ **hdfs dfs -put /tmp/test_data.csv /user/hadoop/test/**

5. execute Hive by : hadoop@nodemaster:/$ **hive**

6. In hive terminal : hive>**create schema if not exists test;**

7. In hive terminal : 

```sql
hive> create external table if not exists test.test_data (row1 int, row2 int, row3 decimal(10,3), row4 int) row format delimited fields terminated by ',' stored as textfile location 'hdfs://172.20.1.1:9000/user/hadoop/test/';
```

8. **Results**
```sql
hive> **select * from test.test_data where row3 > 2.499;
OK
1	122	5.000	838985046
1	185	4.500	838983525
1	231	4.000	838983392
1	292	3.500	838983421
1	316	3.000	838983392
1	329	2.500	838983392
1	377	3.500	838983834
1	420	5.000	838983834
1	466	4.000	838984679
1	480	5.000	838983653
1	520	2.500	838984679
1	539	5.000	838984068
1	586	3.500	838984068
1	588	5.000	838983339
Time taken: 0.175 seconds, Fetched: 14 row(s)
```
