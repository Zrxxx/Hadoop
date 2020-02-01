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
6. 客户端只有访问名称节点才能找到请求的文件块所在的位置。
7. 分布式文件系统通常采用多副本存储，文件块会被复制为多副本，存储在不同的节点上，并且
 存储同一文件块的不同副本的各个节点会分布在不同的机架上。
8. 分布式文件系统的设计需求：透明性、并发控制、文件复制、硬件和操作系统的异构性、
 可伸缩性、容错、安全。
    透明性：用户仅需通过名称节点即可访问数据节点，
        数据节点对用户而言是透明，即用户看不到细节。
    并发控制：客户端对于文件的读写不应该影响其它客户端对同一个文件的读写。
    文件复制：一个文件可以有不同位置的副本
    硬件和操作系统的异构性：客户端和服务端程序的可移植性
    可伸缩性：支持节点的动态加入或退出
9. HDFS采用了“一次写入、多次读取”的简单文件系统，流操作不适合低延迟数据访问。
10. 客户端访问文件->名称节点返回文件的位置列表（文件被分为多个块）->根据数据块找出本地文件并返回客户端。


11. HDFS中，NameNode负责管理分布式文件系统的命名空间namespace，保存了FsImage和EditLog两个数据结构。
  FsImage用于维持文件系统树以及文件树中所有的文件和文件夹的元数据。
  EditLog中记录了所有针对文件的创建、删除、重命名等操作。
12. NameNode启动时，FsImage的内容加载到内存，然后执行EditLog的各项操作，使得内存中的元数据保持最新。
  这个操作完成后，会创建新的FsImage文件和一个空的EditLog文件。
13. DataNode是分布式文件系统HDFS的工作节点，负责数据的存储和读取，定期向NameNode发送自己存储块的列表。
    每个DataNode中的数据会保存在各自节点的本地系统中。
14. Secondary NameNode有效解决EditLog过大，NameNode长期处在更新阶段而不能写入的问题，
    功能：完成FsImage与EditLog的合并，减小EditLog文件大小，缩短NameNode重启时间
         作为NameNode的检查点，保存NameNode中的节点数据。
15. Secondary NameNode与NameNode通讯，要求其停止使用EditLog文件，然后将该时刻t的最新FsImage和EditLog拉到本地，
    由Secondary NameNode进行更新，并将更新完的FsImage发回NameNode，该时刻s,NameNode替换发来的FsImage完成所有更新，
    但s-t时间内，对NameNode的写入操作会缺失。
16. HDFS采用主/从(master/slave)结构模型，NameNode作为中心服务器，DataNode周期性报告自己的状态，没有报告的标记为宕机
17. HDFS的存储原理
