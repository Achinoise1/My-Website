# dockerfile 存档

此文档用于留存一些以前写过的dockerfile内容。

## 2023.12.06

小白对docker的了解不是很多，想拿Readbook上手。最开始以为需要把包括MySQL、Python、nodejs和nginx等所有内容都安装到一个镜像中。后面了解到一个容器干一个事儿的原则之后，就想着拆分原有的内容，但是又担心以后可能会有用，不舍得全部删掉，因此在此存档。

## 拉取基础镜像+署名
```bash
# 拉取centos7.9作为基础镜像
FROM centos:7.9.2009
# 署名
MAINTAINER Achinoise1<today_red@163.com>
```

## 从本机复制文件到镜像中

基本格式是`COPY <src> <dest>`。`\`的作用是换行，有多个文件需要复制的时候建议换行编写，方便阅读。
```bash
# 把要复制的内容都放进去
COPY node-v18.16.0.tar.gz \
    Python-3.8.10.tgz \
    # 以下三行安装包是用来升级gcc/g++的
    centos-release-scl-2-3.el7.centos.noarch.rpm \
    centos-release-scl-rh-2-3.el7.centos.noarch.rpm \
    devtoolset-8-gcc-c++-8.3.1-3.el7.x86_64.rpm \
    nginx-1.20.2-1.el7.ngx.x86_64.rpm /root/
```

## 安装
RUN 指令下进行的操作其实和在终端里运行的操作相似，大部分能在终端运行的操作，都可以写在`RUN`指令中，部分指令除外（如`scl enable devtoolset-8 bash`，该命令必须在bash下操作运行，此时需要更换指令以达到想要的效果）。

需要注意的是，一般在终端下会有提示是否确认安装，用户需要键入 **y/N** 来执行操作。以CentOS为例，`yum install <sth>`需要用户做回应，但是使用dockerfile构建镜像的时候，用户无法键入 y 以确认安装，此时需要将所有`yum install`命令修改为`yum -y install`，即默认确认安装。

### 更新+安装组件/依赖
```bash
RUN su - root \
    && cd /root \
    # 更新
    && yum -y update \
    # 安装wget
    && yum -y install wget \
    # 安装相关依赖
    && yum -y install automake autoconf libtool make \
    && yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel libffi-devel \
    && yum -y install automake autoconf libtool make
```

### 安装MySQL
```bash
RUN su - root \
    && cd /root \
    && wget https://repo.mysql.com//mysql80-community-release-el7-1.noarch.rpm \
    && rpm -ivh mysql80-community-release-el7-1.noarch.rpm \
    && yum -y install mysql mysql-server --nogpgcheck \
    && rm mysql80-community-release-el7-1.noarch.rpm
```

### 安装Python
```bash 
RUN su - root \
    && cd /root \
    && tar xvf Python-3.8.10.tgz \
    && cd Python-3.8*/ \
    && ./configure --prefix=/usr/local/python3  \
    && make \
    && make install \
    && ln -s /usr/local/python3/bin/python3 /usr/bin/python3 \
    && cd .. \
    && rm Python-3.8.10.tgz \
```

```bash
RUN su - root \
    && cd /root \
    && yum -y install nginx-1.20.2-1.el7.ngx.x86_64.rpm \
    && rm nginx-1.20.2-1.el7.ngx.x86_64.rpm
```

### 升级gcc/g++，安装nodejs
```bash
RUN su - root \
    && cd /root \
    && yum -y install gcc gcc-c++ \
    && yum -y install centos-release-scl-rh-2-3.el7.centos.noarch.rpm \
    && yum -y install centos-release-scl-2-3.el7.centos.noarch.rpm \
    && yum -y install devtoolset-8-gcc-c++-8.3.1-3.el7.x86_64.rpm \
    && mv /usr/bin/gcc /usr/bin/gcc-4.8.5 \
    && ln -s /opt/rh/devtoolset-8/root/bin/gcc /usr/bin/gcc \
    && mv /usr/bin/g++ /usr/bin/g++-4.8.5 \
    && ln -s /opt/rh/devtoolset-8/root/bin/g++ /usr/bin/g++ \
    && gcc --version \
    && g++ --version \
    && tar -xf node-v18.16.0.tar.gz \
    && cd node-v18.16.0 \
    && ./configure \
    && make \
    && make install
```

### 安装完成控制台输出
```bash
CMD echo 'custom build finished'
```