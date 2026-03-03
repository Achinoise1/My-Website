# docker compose 下的容器通信

容器是个独立的运行环境，包含文件系统、进程和网络配置等。容器之间的通信通过网络完成。通过网络容器可以在同一台主机或不同的主机上进行通信，实现协同工作。

## docker 容器联网

官方对于 docker 容器联网的解释如下：

> 默认情况下容器开启网络服务，而且能够与外部连接。容器本身并不知道自己连的是哪种网络，也不知道同一个应用的其他服务是否是docker加载的。一个容器只知道自己的IP地址、网关、路由表、DNS服务以及其他的网络配置，除非容器不使用(none)网络驱动。

对于不同的应用程序，可以为对应容器配置合适的网络模式，下面简单介绍 docker 的六种网络模式。

### 六种网络模式

docker 有六种网络模式，分别是 **bridge 模式**、**host 模式**、**none 模式**、**overlay 模式**、**ipvlan 模式**、**macvlan 模式**。

<table>
    <tr>
        <td>网络模式</td>
        <td>解释</td>
        <td>适用情况</td>
    </tr>
    <tr>
        <td>bridge （默认的网络配置）</td>
        <td>docker 为容器创建虚拟网络接口，分配IP地址</td>
        <td>一个主机下的容器之间需要相互通信</td>
    </tr>
    <tr>
        <td>host</td>
        <td>容器网络与宿主机直连，直接使用宿主机的网络</td>
        <td>需要访问主机上的资源/与主机进行高性能通信</td>
    </tr>
    <tr>
        <td>none</td>
        <td>不配置网络，与宿主机和其他容器隔绝</td>
        <td>执行离线任务</td>
    </tr>
    <tr>
        <td>overlay</td>
        <td>将多个 Docker 守护进程连接在一起，容器能够跨节点通信</td>
        <td>分布式应用程序</td>
    </tr>
    <tr>
        <td>ipvlan</td>
        <td>用户可以完全掌控 IPv4 和 IPv6 寻址</td>
        <td>容器之间共享网络命名空间</td>
    </tr>
    <tr>
        <td>macvlan</td>
        <td>允许用户给容器分配 MAC 地址，让它看起来像网络上的物理设备</td>
        <td>容器使用主机网络拥有独立 IP 地址的场景</td>
    </tr>
    <tr>
    <td colspan='3'>内容参考：<br/>1. [Docker6种网络配置详解，网络模式应该这么选]<br/> 2. [Network drivers overview]</td>
    </tr>
</table>

## docker compose 通信：资源文件配置

docker compose 默认为 bridge 网络模式。在没有配置特定网络的情况下使用 docker compose 创建并运行容器，整个服务的所有容器在一个局域网中，每个容器都有一个独立 IP。

对于同一个 YAML 文件，通过 `docker compose down` 删除旧容器后，用 `docker compose up` 创建容器并运行，此时同一服务对应的容器 IP 会发生变化。如果仅仅只是停止容器则不会发生变化。以 nginx 为例，在用 nginx 做代理时，需要在配置文件中填写指定代理的主机，此时有两种选择：写主机的 IP 或者写主机对应的容器名。

### 直接写 IP

笔者在 docker 实战篇首先尝试填写后端容器的 IP，但是直接写 IP 会有一个问题：如果容器遇到问题，无法通过重启容器解决，此时可能需要删除旧容器新起一个容器。那么在 nginx.conf 中写定转发主机的 IP （eg: 192.168.0.2）就不是一个很合适的操作。

```txt
location /api {
    proxy_pass http://192.168.0.2:5000;
}
```

### 写容器名

在访问网站时，浏览器地址栏通常显示的是域名加上相对 URL，而不直接显示 IP 地址。类似地，docker compose 也会为容器配置 DNS 解析。以 nginx 为例，nginx.conf 中的代理主机可以写容器名称而非 IP 地址。写容器名相比写 IP 有一个最直接的好处：容器名都会被解析成容器对应 IP，即便 IP 发生变化也不需要改动 nginx.conf。**笔者推荐使用该种方式配置通信。**

```txt
location /api {
    proxy_pass http://again-readbook-backend:5000;  // 后端容器名称：again-readbook-backend
}
```

[Docker6种网络配置详解，网络模式应该这么选]: https://blog.csdn.net/projim_tao/article/details/129617631
[Network drivers overview]: https://docs.docker.com/network/drivers/