## _3主3从的Redis集群搭建(下)

#### 进入主机6381

> redis-cli -p 6381

![image-20220509100727145](D:\笔记\Docker\part\_3主3从的Redis集群搭建(下).assets\image-20220509100727145.png)

#### 查看集群信息

> cluster info

![image-20220509101055861](D:\笔记\Docker\part\_3主3从的Redis集群搭建(下).assets\image-20220509101055861.png)

查看主机和从机之间的主从关系

> cluster nodes

![image-20220509101455220](D:\笔记\Docker\part\_3主3从的Redis集群搭建(下).assets\image-20220509101455220.png)

