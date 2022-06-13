启动docker
> systemctl start docker

```shell
# 没有任何提示说明启动成功
[root@iZ8vbfaek3x3ogtpxnpnwfZ /]# systemctl start docker
[root@iZ8vbfaek3x3ogtpxnpnwfZ /]#
```

停止docker
> systemctl stop docker

```shell
[root@iZ8vbfaek3x3ogtpxnpnwfZ /]# systemctl stop docker
Warning: Stopping docker.service, but it can still be activated by:
docker.socket
[root@iZ8vbfaek3x3ogtpxnpnwfZ /]
```

查看docker状态
> systemctl status docker

```shell
[root@iZ8vbfaek3x3ogtpxnpnwfZ /]# systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; disabled; vendor preset: disabled)
   Active: inactive (dead) since Mon 2022-04-25 11:21:08 CST; 7s ago
     Docs: https://docs.docker.com
  Process: 11069 ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock (code=exited, status=0/SUCCESS)
 Main PID: 11069 (code=exited, status=0/SUCCESS)
[root@iZ8vbfaek3x3ogtpxnpnwfZ /]
```

重启 docker
> x [root@iZ8vbfaek3x3ogtpxnpnwfZ /]# docker ps --help​Usage:  docker ps [OPTIONS]​List containers​Options:  -a, --all             Show all containers (default shows just running)  -f, --filter filter   Filter output based on conditions provided      --format string   Pretty-print containers using a Go template  -n, --last int        Show n last created containers (includes all states) (default -1)  -l, --latest          Show the latest created container (includes all states)      --no-trunc        Don't truncate output  -q, --quiet           Only display container IDs  -s, --size            Display total file sizes[root@iZ8vbfaek3x3ogtpxnpnwfZ /]#​shell

```shell
# 没有任何提示说明启动成功
[root@iZ8vbfaek3x3ogtpxnpnwfZ /]# systemctl restart docker
[root@iZ8vbfaek3x3ogtpxnpnwfZ /]#
```
