# docker

slug: docker
status: Published
tags: other
type: Post

## docker

https://hub.docker.com/

### 通过docker overlay2 目录名查找对应容器名

```
cd /var/lib/docker/overlay2/
查看容器占用大小
du -s ./* | sort -rn | more
通过目录名查找容器名
docker ps -q | xargs docker inspect --format '{{.State.Pid}}, {{.Id}}, {{.Name}}, {{.GraphDriver.Data.WorkDir}}' | grep bff25099a59b0fc8addd06f9223872f2904256f0432b3c3c47b58faef167115f
```

## docker命令

```
docker启动命令,docker重启命令,docker关闭命令

启动        systemctl start docker

守护进程重启   sudo systemctl daemon-reload

重启docker服务   systemctl restart  docker

重启docker服务  sudo service docker restart

关闭docker service docker stop

关闭docker systemctl stop docker
```