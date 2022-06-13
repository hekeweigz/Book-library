### 查看 镜像/容器/数据 卷所占的空间
> docker system df

```shell
[root@iZ8vbfaek3x3ogtpxnpnwfZ ~]# docker system df
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          6         3         1.173GB   921.1MB (78%)
Containers      6         0         4.517MB   4.517MB (100%)
Local Volumes   0         0         0B        0B
Build Cache     0         0         0B        0B
[root@iZ8vbfaek3x3ogtpxnpnwfZ ~]#

```

### 删除镜像
> docker rmi 镜像ID

```shell
[root@iZ8vbfaek3x3ogtpxnpnwfZ ~]# docker rmi feb5d9fea6a5
Untagged: hello-world:latest
Untagged: hello-world@sha256:2498fce14358aa50ead0cc6c19990fc6ff866ce72aeb5546e1d59caac3d0d60f
Deleted: sha256:feb5d9fea6a5e9606aa995e879d862b825965ba48de054caab5ef356dc6b3412
Deleted: sha256:e07ee1baac5fae6a26f30cabfe54a36d3402f96afda318fe0a96cec4ca393359
[root@iZ8vbfaek3x3ogtpxnpnwfZ ~]#
```
#### 如果提示报错
Error response from daemon: conflict: unable to delete feb5d9fea6a5 (must be forced) - image is being used by stopped container 13111f725991
:::danger
说明之前运行过这个镜像，生成了容器，需要先删除容器，再删除镜像
:::
#### 使用 -f 删除一个
> docker rmi -f 镜像id

#### 使用 -f 删除多个
> docker rmi -f 镜像1：tag 镜像2：tag

#### 使用 -f 删除全部
> docker rmi -f $(docker images -qa)

#### 使用删除容器后删除镜像， 举个栗子
删除已经使用过的hello-world镜像
```shell
[root@iZ8vbfaek3x3ogtpxnpnwfZ ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
tomcat        9.0       b8e65a4d736d   4 months ago    680MB
hello-world   latest    feb5d9fea6a5   7 months ago    13.3kB
centos        latest    5d0da3dc9764   7 months ago    231MB
redis         6.0.8     16ecd2772934   18 months ago   104MB
ubuntu        15.10     9b9cb95443b5   5 years ago     137MB
[root@iZ8vbfaek3x3ogtpxnpnwfZ ~]# docker ps -a
CONTAINER ID   IMAGE          COMMAND              CREATED        STATUS                    PORTS     NAMES
7dae76fcd95b   centos         "/bin/bash"          6 days ago     Exited (0) 6 days ago               distracted_rosalind
b5e8ce2d854d   centos         "/bin/bash"          6 days ago     Exited (0) 6 days ago               naughty_leakey
13111f725991   hello-world    "/hello"             6 days ago     Exited (0) 6 days ago               pensive_liskov
69faadd2d9a4   hello-world    "/hello"             6 days ago     Exited (0) 6 days ago               mystifying_turing
81b542287c10   6b51979725b5   "/.docker_init.sh"   3 months ago   Exited (137) 6 days ago             zentao2
[root@iZ8vbfaek3x3ogtpxnpnwfZ ~]# docker rm 13111f725991
13111f725991
[root@iZ8vbfaek3x3ogtpxnpnwfZ ~]# docker rm 69faadd2d9a4
69faadd2d9a4
[root@iZ8vbfaek3x3ogtpxnpnwfZ ~]# docker rmi feb5d9fea6a5
Untagged: hello-world:latest
Untagged: hello-world@sha256:2498fce14358aa50ead0cc6c19990fc6ff866ce72aeb5546e1d59caac3d0d60f
Deleted: sha256:feb5d9fea6a5e9606aa995e879d862b825965ba48de054caab5ef356dc6b3412
Deleted: sha256:e07ee1baac5fae6a26f30cabfe54a36d3402f96afda318fe0a96cec4ca393359
```

