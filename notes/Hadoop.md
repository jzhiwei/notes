# Hadoop

### HDFS
#### 存储模型
- 文件线性按字节切割成块（block），具有 offset，id
- 文件与文件的 block 大小可以不一样
- 一个文件除最后一个 block，其他 block 大小一样
- block 的大小依据硬件的 IO 特性调整
- block 被分散存放在集群的节点中，具有 location
- block 具有副本（replication），没有主从概念，副本不能出现在同一个节点
- 副本是满足可靠性和性能的关键
- 文件上传可以指定 block 大小和副本数，上传后只能修改副本数
- 一次写入多次读取，不支持修改
- 支持追加数据