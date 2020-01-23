# Hadoop
BigData
1. 分布式文件系统（Distributed File System）是一种通过网络实现文件在多台主机上进行分布式存储的文件系统。
2. 单个计算结点有处理器、内存、高速缓存和本地磁盘构成。
3. Windows、Linus等操作系统中，文件系统一般会把磁盘空间划分为每512字节一组，称为“磁盘块”。文件
系统的块（Block）通常是磁盘块的整数倍。
4. HDFS（Hadoop Distributed File System）默认一个块的大小为64MB。
5. 分布式文件系统在物理结构上由计算机集群中的多个节点构成，节点分为两类：
    一类叫“主节点”(Master Node)或“名称节点”(NameNode)
    另一类叫“从节点”(Slave Node)或"数据节点"(DataNode)
6. 
