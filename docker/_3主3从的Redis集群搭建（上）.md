## _3主3从的`Redis集群`搭建(上)

+ 关闭防火墙，启动docker
+ 新建6个docker容器`docker run -d --name redis-node-6 --net host --privileged=true -v /data/redis/share/redis-node-6:/data redis:6.0.8 --cluster-enabled yes --appendonly yes --port 6386`
  + docker run		创建并运行docker容器实例
  + --name redis-node-6        容器名字
  + --net host        使用宿主机的IP和端口，默认
  + --privileged=true        获取宿主机root用户权限
  + -v /data/redis/share/redis-node-6:/data        容器卷，宿主机地址:docker内部地址
  + redis:6.0.8        redis镜像和版本号
  + --cluster-enabled yes        开启redis集群
  + --appendonly yes        开启持久化
  + --port 6386        redis端口号

```shell
docker run -d --name redis-node-1 --net host --privileged=true -v /data/redis/share/redis-node-1:/data redis:6.0.8 --cluster-enabled yes --appendonly yes --port 6381
docker run -d --name redis-node-2 --net host --privileged=true -v /data/redis/share/redis-node-2:/data redis:6.0.8 --cluster-enabled yes --appendonly yes --port 6382
docker run -d --name redis-node-3 --net host --privileged=true -v /data/redis/share/redis-node-3:/data redis:6.0.8 --cluster-enabled yes --appendonly yes --port 6383
docker run -d --name redis-node-4 --net host --privileged=true -v /data/redis/share/redis-node-4:/data redis:6.0.8 --cluster-enabled yes --appendonly yes --port 6384
docker run -d --name redis-node-5 --net host --privileged=true -v /data/redis/share/redis-node-5:/data redis:6.0.8 --cluster-enabled yes --appendonly yes --port 6385
docker run -d --name redis-node-6 --net host --privileged=true -v /data/redis/share/redis-node-6:/data redis:6.0.8 --cluster-enabled yes --appendonly yes --port 6386
```

运行成功，使用`docker ps`查看

+ 进入容器redis-node-1并为6台机器构建集群关系

  + 进入一台redis进行配置`docker exec -it redis-node-1 bash `

  + ```shell
    #进入后执行
    redis-cli --cluster create 8.142.144.75:6381 8.142.144.75:6382 8.142.144.75:6383 8.142.144.75:6384 8.142.144.75:6385 8.142.144.75:6386 --cluster-replicas 1
    
     --cluster create	构建集群
     --cluster-replicas 1	集群关联一比一的关系
     
    --cluster-replicas 1 表示为每个master创建一个slave节点
    # 注意：上面的ip为真实IP
    ```

  有下面的绿色ok字样显示运行成功

  ![image-20220507145226431](D:\笔记\Docker\part\_3主3从的Redis集群搭建（上）.assets\image-20220507145226431.png)

  > 如果运行不成功，一直显示`Waiting for the cluster to join.. `一直........................................，则是端口没有全部开放，防火墙也要开放端口，以阿里云为例

  就是需要在安全组上面配置6381~6386的6个端口，<font color="red">还需要配置16381~16386的6个端口</font>，共12个端口都要开放，不然会一直提示等待

  + 一切OK的话，3主3从搭建搞定

