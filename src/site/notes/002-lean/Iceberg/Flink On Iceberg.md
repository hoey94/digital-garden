---
{"dg-publish":true,"permalink":"/002-lean/Iceberg/Flink On Iceberg/","dgPassFrontmatter":true}
---



## **5.1 环境准备**

### **5.1.1 安装 Flink**

**1）Flink与Iceberg的版本对应关系如下**

| Flink 版本 | Iceberg 版本      |
|----------|-----------------|
| 1.11     | 0.9.0 – 0.12.1  |
| 1.12     | 0.12.0 – 0.13.1 |
| 1.13     | 0.13.0 – 1.0.0  |
| 1.14     | 0.13.0 – 1.1.0  |
| 1.15     | 0.14.0 – 1.1.0  |
| 1.16     | 1.1.0 – 1.1.0   |

  

**2）上传并解压Flink安装包**

```shell
tar -zxvf flink-1.16.0-bin-scala\_2.12.tgz -C /opt/module/
```  

**3）配置环境变量**

  ```shell
  sudo vim /etc/profile.d/my\_env.sh
  export HADOOP\_CLASSPATH=`hadoop classpath`
  source /etc/profile.d/my\_env.sh
```

**4）拷贝iceberg的jar包到Flink的lib目录**

```shell
cp /opt/software/iceberg/iceberg-flink-runtime-1.16-1.1.0.jar /opt/module/flink-1.16.0/lib
```

### **5.1.2 启动 Hadoop**

（略）

### **5.1.3 启动 sql-client**

**1）修改flink-conf.yaml配置**

```shell

vim /opt/module/flink-1.16.0/conf/flink-conf.yaml

classloader.check-leaked-classloader: false
taskmanager.numberOfTaskSlots: 4
state.backend: rocksdb
execution.checkpointing.interval: 30000
state.checkpoints.dir: hdfs://hadoop1:8020/ckps
state.backend.incremental: true
```

**2）local模式**

（1）修改workers

  ```shell
  vim /opt/module/flink-1.16.0/conf/workers

#表示：会在本地启动3个TaskManager的 local集群
localhost
localhost
localhost
```


（2）启动Flink

```shell
/opt/module/flink-1.16.0/bin/start-cluster.sh
```

查看webui：http://hadoop1:8081

（3）启动Flink的sql-client

```shell
/opt/module/flink-1.16.0/bin/sql-client.sh embedded
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240531171354.png)


## **5.2 创建和使用 Catalog**

### **5.2.1 语法说明**

```sql
CREATE CATALOG <catalog_name> WITH (
  'type'='iceberg',
  `<config_key>`=`<config_value>`
);
```


- type: 必须是iceberg。（必须）

- catalog-type: 内置了hive和hadoop两种catalog，也可以使用catalog-impl来自定义catalog。（可选）

- catalog-impl: 自定义catalog实现的全限定类名。如果未设置catalog-type，则必须设置。（可选）

- property-version: 描述属性版本的版本号。此属性可用于向后兼容，以防属性格式更改。当前属性版本为1。（可选）

- cache-enabled: 是否启用目录缓存，默认值为true。（可选）

- cache.expiration-interval-ms: 本地缓存catalog条目的时间(以毫秒为单位)；负值，如-1表示没有时间限制，不允许设为0。默认值为-1。（可选）

### **5.2.2 Hive Catalog**

**1）上传hive connector到flink的lib中**

```shell
cp flink-sql-connector-hive-3.1.2\_2.12-1.16.0.jar /opt/module/flink-1.16.0/lib/
```
  
**2）启动hive metastore服务**

  ```shell
hive --service metastore  
```


**3）创建hive catalog**

重启flink集群，重新进入sql-client

  ```sql
CREATE CATALOG hive_catalog WITH (
  'type'='iceberg',
  'catalog-type'='hive',
  'uri'='thrift://hadoop1:9083',
  'clients'='5',
  'property-version'='1',
  'warehouse'='hdfs://hadoop1:8020/warehouse/iceberg-hive'
);

use catalog hive_catalog;
```


- uri: Hive metastore的thrift uri。(必选)

- clients:Hive metastore客户端池大小，默认为2。(可选)

- warehouse: 数仓目录。

- hive-conf-dir:包含hive-site.xml配置文件的目录路径，hive-site.xml中hive.metastore.warehouse.dir 的值会被warehouse覆盖。

- hadoop-conf-dir:包含core-site.xml和hdfs-site.xml配置文件的目录路径。

### **5.2.3 Hadoop Catalog**

Iceberg还支持HDFS中基于目录的catalog，可以使用'catalog-type'='hadoop'配置。

  ```sql
CREATE CATALOG hadoop_catalog WITH (
  'type'='iceberg',
  'catalog-type'='hadoop',
  'warehouse'='hdfs://hadoop1:8020/warehouse/iceberg-hadoop',
  'property-version'='1'
);
use catalog hadoop_catalog;
```
  
- warehouse:存放元数据文件和数据文件的HDFS目录。（必需）

### **5.2.4 配置sql-client初始化文件**

```sql
vim /opt/module/flink-1.16.0/conf/sql-client-init.sql

CREATE CATALOG hive_catalog WITH (
  'type'='iceberg',
  'catalog-type'='hive',
  'uri'='thrift://hadoop1:9083',
  'warehouse'='hdfs://hadoop1:8020/warehouse/iceberg-hive'
);
USE CATALOG hive_catalog;
```

后续启动sql-client时，加上 -i sql文件路径 即可完成catalog的初始化。

```shell
/opt/module/flink-1.16.0/bin/sql-client.sh embedded -i conf/sql-client-init.sql
```


## **5.3 DDL 语句**

### **5.3.1 创建数据库**
```sql
CREATE DATABASE iceberg_db;
USE iceberg_db;
```

### **5.3.2 创建表**
```sql
CREATE TABLE `hive_catalog`.`default`.`sample` (
    id BIGINT COMMENT 'unique id',
    data STRING
);
```

建表命令现在支持最常用的flink建表语法，包括:

- PARTITION BY (column1, column2, ...)：配置分区，apache flink还不支持隐藏分区。

- COMMENT 'table document'：指定表的备注

- WITH ('key'='value', ...)：设置表属性

目前，不支持计算列、watermark（支持主键）。

**1）创建分区表**

  ```sql
  CREATE TABLE `hive_catalog`.`default`.`sample` (
    id BIGINT COMMENT 'unique id',
    data STRING
) PARTITIONED BY (data);
```

Apache Iceberg支持隐藏分区，但Apache flink不支持在列上通过函数进行分区，现在无法在flink DDL中支持隐藏分区。

**2）使用LIKE语法建表**


LIKE语法用于创建一个与另一个表具有相同schema、分区和属性的表。

  ```sql
  CREATE TABLE `hive_catalog`.`default`.`sample` (
    id BIGINT COMMENT 'unique id',
    data STRING
);
CREATE TABLE  `hive_catalog`.`default`.`sample_like` LIKE `hive_catalog`.`default`.`sample`;
```

### **5.3.3 修改表**

**1）修改表属性**
```sql
ALTER TABLE `hive_catalog`.`default`.`sample` SET ('write.format.default'='avro');
```

**2）修改表名**

  ```sql
ALTER TABLE `hive_catalog`.`default`.`sample` RENAME TO `hive_catalog`.`default`.`new_sample`;
```

### **5.3.4 删除表**

```sql
DROP TABLE `hive_catalog`.`default`.`sample`;
```

## **5.4 插入语句**

### **5.4.1 INSERT INTO**

```sql
INSERT INTO `hive_catalog`.`default`.`sample` VALUES (1, 'a');

INSERT INTO `hive_catalog`.`default`.`sample` SELECT id, data from sample2;
```

### **5.4.2 INSERT OVERWRITE**

仅支持Flink的Batch模式

  ```sql
SET execution.runtime-mode = batch;
INSERT OVERWRITE sample VALUES (1, 'a');
INSERT OVERWRITE `hive_catalog`.`default`.`sample` PARTITION(data='a') SELECT 6;
```


### **5.4.3 UPSERT**

当将数据写入v2表格式时，Iceberg支持基于主键的UPSERT。有两种方法可以启用upsert。

**1）建表时指定**

```sql
CREATE TABLE `hive_catalog`.`test1`.`sample5` (
  `id`  INT UNIQUE COMMENT 'unique id',
  `data` STRING NOT NULL,
PRIMARY KEY(`id`) NOT ENFORCED
) with (
'format-version'='2',
'write.upsert.enabled'='true'
);
```

**2）插入时指定**

  ```sql
  INSERT INTO tableName /*+ OPTIONS('upsert-enabled'='true') */...
```

插入的表，format-version需要为2。

OVERWRITE和UPSERT不能同时设置。在UPSERT模式下，如果对表进行分区，则分区字段必须也是主键。

**3）读取Kafka流，upsert插入到iceberg表中**

  ```sql
create table default_catalog.default_database.kafka(
  id int,
  data string
) with (
  'connector' = 'kafka'
  ,'topic' = 'test111'
  ,'properties.zookeeper.connect' = 'hadoop1:2181'
  ,'properties.bootstrap.servers' = 'hadoop1:9092'
  ,'format' = 'json'
  ,'properties.group.id'='iceberg'
  ,'scan.startup.mode'='earliest-offset'
);
INSERT INTO hive_catalog.test1.sample5 SELECT * FROM default_catalog.default_database.kafka;
```


## **5.5 查询语句**

Iceberg支持Flink的流式和批量读取。

### **5.5.1 Batch模式**

```sql
SET execution.runtime-mode = batch;
select * from sample;
```


### **5.5.2 Streaming模式**

```sql
SET execution.runtime-mode = streaming;
SET table.dynamic-table-options.enabled=true;
SET sql-client.execution.result-mode=tableau;
```

  

**1）从当前快照读取所有记录，然后从该快照读取增量数据**

  ```sql
SELECT * FROM sample5 /*+ OPTIONS('streaming'='true', 'monitor-interval'='1s')*/ ;
```


**2）读取指定快照id（不包含）后的增量数据**

  
```sql
SELECT * FROM sample /*+ OPTIONS('streaming'='true', 'monitor-interval'='1s', 'start-snapshot-id'='3821550127947089987')*/ ;
```

- monitor-interval: 连续监控新提交数据文件的时间间隔（默认为10s）。

- start-snapshot-id: 流作业开始的快照id。

  

**注意：**如果是无界数据流式upsert进iceberg表（读kafka，upsert进iceberg表），那么再去流读iceberg表会存在读不出数据的问题。如果无界数据流式append进iceberg表（读kafka，append进iceberg表），那么流读该iceberg表可以正常看到结果。

## **5.6 与Flink集成的不足**

  
| 支持的特性                 | Flink | 备注                      |
|-----------------------|-------|-------------------------|
| SQL create catalog    | √     |                         |
| SQL create database   | √     |                         |
| SQL create table      | √     |                         |
| SQL create table like | √     |                         |
| SQL alter table       | √     | 只支持修改表属性，不支持更改列和分区      |
| SQL drop_table        | √     |                         |
| SQL select            | √     | 支持流式和批处理模式              |
| SQL insert into       | √     | 支持流式和批处理模式              |
| SQL insert overwrite  | √     |                         |
| DataStream read       | √     |                         |
| DataStream append     | √     |                         |
| DataStream overwrite  | √     |                         |
| Metadata tables       |       | 支持Java API，不支持Flink SQL |
| Rewrite files action  | √     |


- 不支持创建隐藏分区的Iceberg表。

- 不支持创建带有计算列的Iceberg表。

- 不支持创建带watermark的Iceberg表。

- 不支持添加列，删除列，重命名列，更改列。

- Iceberg目前不支持Flink SQL 查询表的元数据信息，需要使用Java API 实现。

# **第6章 与 Flink DataStream 集成**

## **6.1 环境准备**

### **6.1.1 配置pom文件**

新建Maven工程，pom文件配置如下：

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.atguigu.iceberg</groupId>
    <artifactId>flink-iceberg-demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <flink.version>1.16.0</flink.version>
        <java.version>1.8</java.version>
        <scala.binary.version>2.12</scala.binary.version>
        <slf4j.version>1.7.30</slf4j.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-java</artifactId>
            <version>${flink.version}</version>
            <scope>provided</scope>   <!--不会打包到依赖中，只参与编译，不参与运行 -->
        </dependency>
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-streaming-java</artifactId>
            <version>${flink.version}</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-clients</artifactId>
            <version>${flink.version}</version>
            <scope>provided</scope>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.apache.flink/flink-table-planner -->
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-table-planner_${scala.binary.version}</artifactId>
            <version>${flink.version}</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-connector-files</artifactId>
            <version>${flink.version}</version>
            <scope>provided</scope>
        </dependency>
        <!--idea运行时也有webui-->
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-runtime-web</artifactId>
            <version>${flink.version}</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>${slf4j.version}</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>${slf4j.version}</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-to-slf4j</artifactId>
            <version>2.14.0</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-statebackend-rocksdb</artifactId>
            <version>${flink.version}</version>
        </dependency>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>3.1.3</version>
            <scope>provided</scope>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.apache.iceberg/iceberg-flink-runtime-1.16 -->
        <dependency>
            <groupId>org.apache.iceberg</groupId>
            <artifactId>iceberg-flink-runtime-1.16</artifactId>
            <version>1.1.0</version>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.2.4</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <artifactSet>
                                <excludes>
                                    <exclude>com.google.code.findbugs:jsr305</exclude>
                                    <exclude>org.slf4j:*</exclude>
                                    <exclude>log4j:*</exclude>
                                    <exclude>org.apache.hadoop:*</exclude>
                                </excludes>
                            </artifactSet>
                            <filters>
                                <filter>
                                    <!-- Do not copy the signatures in the META-INF folder.
                                    Otherwise, this might cause SecurityExceptions when using the JAR. -->
                                    <artifact>*:*</artifact>
                                    <excludes>
                                        <exclude>META-INF/*.SF</exclude>
                                        <exclude>META-INF/*.DSA</exclude>
                                        <exclude>META-INF/*.RSA</exclude>
                                    </excludes>
                                </filter>
                            </filters>
                            <transformers combine.children="append">
                                <transformer
                                        implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
                                </transformer>
                            </transformers>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```


### **6.1.2 配置log4j**

```
log4j.rootLogger=error,stdout
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.target=System.out
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d %p [%c] - %m%n
```


## **6.2 读取数据**

### **6.2.1 常规Source写法**

**1）Batch方式**
```java
StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
TableLoader tableLoader = TableLoader.fromHadoopTable("hdfs://hadoop1:8020/warehouse/spark-iceberg/default/a");
DataStream<RowData> batch = FlinkSource.forRowData()
     .env(env)
     .tableLoader(tableLoader)
     .streaming(false)
     .build();
batch.map(r -> Tuple2.of(r.getLong(0),r.getLong(1) ))
      .returns(Types.TUPLE(Types.LONG,Types.LONG))
      .print();
env.execute("Test Iceberg Read");
```
  


**2）Streaming方式**

  
```java
StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
TableLoader tableLoader = TableLoader.fromHadoopTable("hdfs://hadoop1:8020/warehouse/spark-iceberg/default/a");
DataStream<RowData> stream = FlinkSource.forRowData()
     .env(env)
     .tableLoader(tableLoader)
     .streaming(true)
     .startSnapshotId(3821550127947089987L)
     .build();
stream.map(r -> Tuple2.of(r.getLong(0),r.getLong(1) ))
      .returns(Types.TUPLE(Types.LONG,Types.LONG))
      .print();
env.execute("Test Iceberg Read");
```


### **6.2.2 FLIP-27 Source写法**

**1）Batch方式**
```java
   StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
	TableLoader tableLoader = TableLoader.fromHadoopTable("hdfs://hadoop1:8020/warehouse/spark-iceberg/default/a");
	IcebergSource<RowData> source1 = IcebergSource.forRowData()
			.tableLoader(tableLoader)
			.assignerFactory(new SimpleSplitAssignerFactory())
			.build();
	DataStream<RowData> batch = env.fromSource(
			Source1,
			WatermarkStrategy.noWatermarks(),
			"My Iceberg Source",
			TypeInformation.of(RowData.class));
	batch.map(r -> Tuple2.of(r.getLong(0), r.getLong(1)))
			.returns(Types.TUPLE(Types.LONG, Types.LONG))
			.print();
	env.execute("Test Iceberg Read");
```
  

**2）Streaming方式**

  ```java
  StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
	TableLoader tableLoader = TableLoader.fromHadoopTable("hdfs://hadoop1:8020/warehouse/spark-iceberg/default/a");
	IcebergSource source2 = IcebergSource.forRowData()
			.tableLoader(tableLoader)
			.assignerFactory(new SimpleSplitAssignerFactory())
			.streaming(true)
			.streamingStartingStrategy(StreamingStartingStrategy.INCREMENTAL_FROM_LATEST_SNAPSHOT)
			.monitorInterval(Duration.ofSeconds(60))
			.build();
	DataStream<RowData> stream = env.fromSource(
			Source2,
			WatermarkStrategy.noWatermarks(),
			"My Iceberg Source",
			TypeInformation.of(RowData.class));
	stream.map(r -> Tuple2.of(r.getLong(0), r.getLong(1)))
			.returns(Types.TUPLE(Types.LONG, Types.LONG))
			.print();
	env.execute("Test Iceberg Read");
	
```


## **6.3 写入数据**

目前支持DataStream中RowData和DataStream中Row格式的数据流写入Iceberg表。


**1）写入方式支持 append、overwrite、upsert**

```java
StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
env.setParallelism(1);
        SingleOutputStreamOperator<RowData> input = env.fromElements("")
                .map(new MapFunction<String, RowData>() {
                    @Override
                    public RowData map(String s) throws Exception {
                        GenericRowData genericRowData = new GenericRowData(2);
                        genericRowData.setField(0, 99L);
                        genericRowData.setField(1, 99L);
                        return genericRowData;
                    }
                });
        TableLoader tableLoader = TableLoader.fromHadoopTable("hdfs://hadoop1:8020/warehouse/spark-iceberg/default/a");
FlinkSink.forRowData(input)
.tableLoader(tableLoader)
.append()            // append方式
//.overwrite(true)   // overwrite方式
//.upsert(true)       // upsert方式
            ;
env.execute("Test Iceberg DataStream");
```

  

**2）写入选项**

  ```java
  FlinkSink.forRowData(input)
    .tableLoader(tableLoader)
    .set("write-format", "orc")
    .set(FlinkWriteOptions.OVERWRITE_MODE, "true");
```
  

可配置选项如下：

| 选项                     | 默认值                                    | 说明                                 |
|------------------------|----------------------------------------|------------------------------------|
| write-format           | Parquet                                | 写入操作使用的文件格式：Parquet, avro或orc      |
|                        | 同write.format.default                  |                                    |
| target-file-size-bytes | 536870912（512MB）                       | 控制生成的文件的大小，目标大约为这么多字节              |
|                        | 同write.target-file-size-bytes          |                                    |
| upsert-enabled         | 同write.upsert.enabled，                 |                                    |
|                        |                                        |                                    |
| overwrite-enabled      | FALSE                                  | 覆盖表的数据，不能和UPSERT模式同时开启             |
| distribution-mode      | None                                   | 定义写数据的分布方式:                        |
|                        | 同 write.distribution-mode              | Ø none:不打乱行;                       |
|                        |                                        | Ø hash:按分区键散列分布;                   |
|                        |                                        | Ø range：如果表有SortOrder，则通过分区键或排序键分配 |
| compression-codec      | 同 write.(fileformat).compression-codec |                                    |
| compression-level      | 同 write.(fileformat).compression-level |                                    |
| compression-strategy   | 同write.orc.compression-strategy        |




## **6.4 合并小文件**

Iceberg现在不支持在flink sql中检查表，需要使用Iceberg提供的Java API来读取元数据来获得表信息。可以通过提交Flink批处理作业将小文件重写为大文件：

  ```java
  import org.apache.iceberg.flink.actions.Actions;
        // 1.获取 Table对象
        // 1.1 创建 catalog对象
        Configuration conf = new Configuration();
        HadoopCatalog hadoopCatalog = new HadoopCatalog(conf, "hdfs://hadoop1:8020/warehouse/spark-iceberg");
        // 1.2 通过 catalog加载 Table对象
        Table table = hadoopCatalog.loadTable(TableIdentifier.of("default", "a"));
        // 有Table对象，就可以获取元数据、进行维护表的操作
//        System.out.println(table.history());
//        System.out.println(table.expireSnapshots().expireOlderThan());
        // 2.通过 Actions 来操作 合并
        Actions.forTable(table)
                .rewriteDataFiles()
                .targetSizeInBytes(1024L)
                .execute();
```


得到Table对象，就可以获取元数据、进行维护表的操作。更多Iceberg提供的API操作，参考：https://iceberg.apache.org/docs/latest/api/
