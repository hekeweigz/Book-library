## redis的4主4从缩容

##### 目的：6387和6388下线

##### 检查集群情况获得6388的节点ID

> redis-cli --cluster check 8.142.144.75:6382

![image-20220509172354404](D:\笔记\Docker\part\redis的4主4从缩容.assets\image-20220509172354404.png)

##### 从集群中将4号从节点6388删除

> redis-cli --cluster del-node ip:从机端口 从机6388节点ID

![image-20220509172850125](D:\笔记\Docker\part\redis的4主4从缩容.assets\image-20220509172850125.png)

##### 使用`redis-cli --cluster check 8.142.144.75:6382`进行集群检查

![image-20220509173130464](D:\笔记\Docker\part\redis的4主4从缩容.assets\image-20220509173130464.png)

6388删除成功

##### 将6387的槽号清空，重新分配

本例将清出来的槽号都给6381

使用`redis-cli --cluster reshard ip:6381`进行节点的重组

![image-20220509174702772](D:\笔记\Docker\part\redis的4主4从缩容.assets\image-20220509174702772.png)

<font color="red">注：</font>

上图中1输入的4096是6387主机所拥有的槽点数量，把他们全部拿出来分掉

上图的2输入的ID是<font color="red">接收</font>6387主机所放出的槽点数的主机id

上图中3输入的ID是<font color="red">放出</font>槽点数的6387主机的id

上图中4输入的done指的是已经输入完所有的节点

##### 使用`redis-cli --cluster check 8.142.144.75:6382`进行集群检查

![image-20220509175720067](D:\笔记\Docker\part\redis的4主4从缩容.assets\image-20220509175720067.png)

##### 删除6387节点的主机

> redis-cli --cluster del-node ip:端口 6387节点ID

![image-20220509180111949](D:\笔记\Docker\part\redis的4主4从缩容.assets\image-20220509180111949.png)

##### 使用`redis-cli --cluster check 8.142.144.75:6382`进行集群检查

![image-20220509180222538](D:\笔记\Docker\part\redis的4主4从缩容.assets\image-20220509180222538.png)