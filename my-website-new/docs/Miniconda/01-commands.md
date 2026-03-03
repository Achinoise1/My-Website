# 常用指令

## 创建新虚拟环境

当有新的 proj 需要创建新环境用于测试时，可以使用如下命令创建虚拟环境  
此时的 python 环境为系统默认的python环境(CentOS, 2.7.5)。
```bash
conda create --name <env name>
```

如果系统默认的python环境符合开发需求，则可以按照上述命令运行。  
否则进入到虚拟环境中重新配置python环境会比较复杂，推荐直接创建虚拟环境时直接配置python版本。

```bash
conda create --name <env name> python=<version>
# eg: conda create --name regexTest python=3.8.10
```

## 删除虚拟环境

由于配错环境或者其他等等原因不再需要该虚拟环境时，可用如下命令删除虚拟环境：
```bash
conda env remove --name <env name>
# eg: conda env remove --name regexTest
```

删除时请确保当前位置环境不是删除的目标环境，否则删除失败  
删除的目标环境需要deactivate，否则同样删除失败

## 启用指定虚拟环境
进入系统后默认在base中，如果需要进入指定环境，使用如下命令：
```bash
conda activate <env name>
# eg: conda activate regexTest
```

● 疑问：如果当前不在base环境，而是在虚拟环境1下，启用一个虚拟环境2，此时虚拟环境1会自动deactivate，然后进入虚拟环境2？还是虚拟环境1还是处于activate状态？  
● 答：虚拟环境1会自动deactivate并进入虚拟环境2，此时想要删除虚拟环境1可以正常操作。但是还有一个很奇怪的点，此时退出虚拟环境2，系统会回退到虚拟环境1而不是base。再继续deactivate才是base。

## 退出虚拟环境

当不需要再使用该环境时，使用如下命令退出环境，回到base中：

```bash
conda deactivate
```

## 查看安装的所有环境

```bash
conda info --envs
```

## 增加channel
在使用 miniconda 时，直接用 Anaconda 官方渠道可能速度较慢，因此会添加国内镜像源。  
注意这个镜像指的是<b> conda 的镜像</b>，请务必与 python 安装库的镜像区分开。  
如果在 conda channel 中添加 python 安装库的镜像会导致后续 conda 创建虚拟环境等操作出错。  
具体命令如下：
```bash
conda config --add channels <channel-url>
# eg: conda config --add channels https://mirrors.aliyun.com/anaconda/pkgs/main/
```

添加完毕之后可用一下命令查看所有channel：

```bash
conda config --show
```

## 删除channel

可能存在添加时channel url填写错误，导致后续创建/删除虚拟环境等操作无法进行的情况  
需要删除已有的channel，可执行如下命令：
```bash
conda config --remove channels <channel-name>
```