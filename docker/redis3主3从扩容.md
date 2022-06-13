## redis的3主3从扩容

#### 首先添加两个redis

```shell
# 创建redis-node-7
docler run -d --name redis-node-7 --net host --privileged=true -v /data/redis/share/redis-node-7:/data redis:6.0.8 --cluster-enabled yes --appendonly yes --port 6387
# 创建redis-node-8
docler run -d --name redis-node-8 --net host --privileged=true -v /data/redis/share/redis-node-8:/data redis:6.0.8 --cluster-enabled yes --appendonly yes --port 6388
```

<font color="green">注：在阿里云的安全组和防火墙上添加6387,16387 6388,16388四个端口</font>

#### 配置步骤：

##### 执行`docker exec -it redis-node-1 bash `进入redis-node-1里面

##### 执行`redis-cli --cluster add-node 8.142.144.75:6387 8.142.144.75:6381`

![image-20220509161917941](D:\笔记\Docker\part\redis3主3从扩容.assets\image-20220509161917941.png)

6387	新加入的节点

6381	相当于6387的领路人

##### 使用`redis-cli --cluster check 8.142.144.75:6381`检查

![image-20220509162146380](D:\笔记\Docker\part\redis3主3从扩容.assets\image-20220509162146380.png)

##### 重新分配槽号

> redis-cli --cluster reshard IP地址:端口号

![image-20220509164304608](D:\笔记\Docker\part\redis3主3从扩容.assets\image-20220509164304608.png)

<font color="red">注：上图的1指的是：对主机数平分16384个节点，16384/主机数（包含想要添加的主机）</font>

<font color="red">注：上图的2指的是：新加入的6387节点的ID</font>

​				![image-20220509164445562](D:\笔记\Docker\part\redis3主3从扩容.assets\image-20220509164445562.png)

<font color="red">all：表示全部进行重新分配</font>

在重新加载过程会碰到`Do you want to proceed with the proposed reshard plan (yes/no)?`一句话，选择yes就可以

<img src="D:\笔记\Docker\part\redis3主3从扩容.assets\image-20220509165333288.png" alt="image-20220509165333288"  />

##### 检查集群情况

![image-20220509165711542](D:\笔记\Docker\part\redis3主3从扩容.assets\image-20220509165711542.png)

##### 为主节点6387分配从节点6388

> redis-cli --cluster add-node ip:新slave端口 ip:新master端口 --cluster-slave --cluster-master-id 新主机节点ID

![image-20220509171001762](D:\笔记\Docker\part\redis3主3从扩容.assets\image-20220509171001762.png)

##### 检查集群情况

> redis-cli --cluster check 8.142.144.75:6382

![image-20220509171227600](D:\笔记\Docker\part\redis3主3从扩容.assets\image-20220509171227600.png)

