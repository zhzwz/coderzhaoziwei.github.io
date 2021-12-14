docker 容器 自动重启

docker run [Container ID] --restart unless-stopped
docker run [Container ID] --restart always

docker run 064b84fe81ab --restart unless-stopped



docker ps -a | grep Exited | awk '{print $1}' |xargs docker start

### 一条命令重启所有已停止的容器

- 查看 docker 所有已停止的容器

```
docker ps -a | grep Exited
```

- 获取停止的容器 id（使用 `cut` 或 `awk`）

```
docker ps -a | grep Exited | cut -d' ' -f1
docker ps -a | grep Exited | awk '{print $1}'
```

- 将已停止的容器 id 作为参数传给启动命令

```
docker ps -a | grep Exited | awk '{print $1}' |xargs docker start
```

> `xargs` 可以将前面命令得到的结果作为参数传递给下个命令

@see https://blog.csdn.net/qq_39314099/article/details/105785134
