# Docker 命令合集
在学docker的时候，网站[Docker从入门到实践]给出了很详细的讲解，这里仅作命令记录，想不起来命令的时候方便快速查找使用

## 通用
### 查看版本

```bash
docker --version
```

### 查看运行情况

```bash
systemctl status docker
```

### 启动docker

```bash
sudo systemctl start docker
```

### 查看占用大小

```bash
docker system df [-v]
```

### 一键清除

```bash
docker system prune
```

此时会清除如下内容：
```bash
WARNING! This will remove:
  - all stopped containers                              # 已停止运行的容器
  - all networks not used by at least one container     # 无用的网络
  - all dangling images                                 # 虚悬镜像
  - all dangling build cache                            # 虚悬构建缓存
```

虚悬镜像指的是那些无标签的镜像，即使用 `docker image ls` 能看到 `<none>:<none>` 的镜像。虚悬镜像生成的原因可能有两个，一是构建镜像的时候没有指定命名；二是出现相同标签的镜像。在已有标签 `<name>:<tag>` 镜像的情况下，如果 build 一个 `<name>:<tag>` 镜像，此时docker会将旧镜像的标签更新为 `<none>:<none>` ，新镜像为 `<name>:<tag>` 。

## 镜像
### 获取镜像

```bash
docker pull <name>:<tag>
# eg: docker pull ubuntu:18.04
```

### 用Dockerfile构建镜像

```bash
docker build -f <Dockerfile name> -t <image name> ./
```

## 容器
### 列出容器

```bash
docker ps [-a]
docker container ls [-a]
```

-a: 显示所有容器，包括未运行的容器

### 删除指定ID容器

```bash
docker rm -f <container id前三位>
```

### 删除已停止的容器

```bash
docker container prune
```

### 新建容器并启动

```bash
docker run <image>
```

<table>
    <thead>
        <tr>
            <th style={{width: '20%'}}>可选项</th>
            <th style={{width: '25%'}}>含义</th>
            <th style={{width: '35%'}}>用法</th>
            <th style={{width: '20%'}}>示例</th>
        </tr>
    </thead>
    <tbody >
        <tr >
            <td>--name</td>
            <td>命名容器</td>
            <td>`docker run --name <name> <image>`</td>
            <td>`docker run --name webserver nginx`</td>
        </tr>
        <tr >
            <td>-d<br/>--detach</td>
            <td>在后台运行容器并在控制台输出容器的ID</td>
            <td>`docker run -d`</td>
            <td>同左</td>
        </tr>
        <tr >
            <td>-p<br/>--publish list</td>
            <td>指定端口映射</td>
            <td>`docker run -p <host port>:<container port>`</td>
            <td>`docker run -p 81:80`</td>
        </tr>
    </tbody>
</table>  

新建容器并进入到容器的终端中，退出容器终端视为容器停止
```bash
docker run -t -i <image name> /bin/bash
```

### 进入指定容器

根据容器名称
```bash
docker exec -i -t <container name> /bin/bash
```

根据容器ID
```bash
docker exec -it <container id> /bin/bash
```

### 停止容器

```bash
docker kill <container name>
docker container stop <container id>
```

[Docker从入门到实践]:https://vuepress.mirror.docker-practice.com/

### 查看容器日志

```bash
docker logs <container id>
```

### 不进入容器执行指定命令

```bash
docker exec <container id> <command>
# eg: docker exec 91c nginx
```
## 网络

### 查看内建的网络列表

```bash
docker network ls
```

### 宿主机查看容器内部端口占用情况
```bash
docker port <container id>
```

## compose

### 构建+起容器

```bash
docker compose -f <yml file name> up -d
```

-d：容器在后台运行

此时可以逐行执行命令进入到容器中

```bash
docker container ls -a                      # 找到刚起的容器
docker exec -it <container id> /bin/bash    # 进入容器
```


### 关闭+删除容器

```bash
docker compose -f <yml file> down
```

### 关闭容器(不删除)

```bash
docker compose -f <yml file> stop
```