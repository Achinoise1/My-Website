# 安装软件

针对 Ubuntu 22.04 版本。

## MySQL

### 安装
依次执行如下命令：
```bash
sudo apt update
sudo apt install mysql-server -y
```

### 启动服务
```bash
sudo systemctl enable mysql
sudo systemctl status mysql
sudo mysql
```

进入 mysql。

### 设置密码
```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '<password>';
FLUSH PRIVILEGES;
exit
```

设置完成后，再次登录使用如下命令

```bash
sudo mysql -u root -p
```

## Miniconda

### bug

按照官网执行，但执行 `conda --version` 出现报错： `conda: command not found`，编辑 `~/.bashrc` 文件，在文件末尾加上：

```bash
# export PATH=$PATH:<安装miniconda的位置>
export PATH=$PATH:/root/miniconda3/bin
```

保存后退出，执行 `source ~/.bashrc`。此时再次执行 `conda --version`，能够查看当前 conda 版本。

## Nodejs

如果直接使用 `sudo apt-get install nodejs`，安装的版本为 v12，且不带 npm，因此使用如下方式安装。

### 彻底卸载

```bash
sudo apt purge --autoremove nodejs npm
```

### 安装

```bash
sudo apt install git curl
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
```

安装完成后执行 `node -v` 和 `npm -v` 能分别查看对应版本，则安装成功。
