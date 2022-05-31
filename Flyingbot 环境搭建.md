# Flyingbot 环境搭建

https://github.com/columbia-ai-robotics/flingbot

## Docker

### Dockerfile

- FROM 指定基础镜像

所谓定制镜像，那一定是以一个镜像为基础，在其上进行定制。基础镜像是必须指定的。而 `FROM` 就是指定 **基础镜像**，因此一个 `Dockerfile` 中 `FROM` 是必备的指令，并且必须是第一条指令。

[Docker下载包的时候显示Connection failed]: https://blog.csdn.net/AlexNbZou/article/details/122731255

Dockerfile FROM ***下面，加上以下代码：

```bash
RUN sed -i s:/archive.ubuntu.com:/mirrors.tuna.tsinghua.edu.cn/ubuntu:g /etc/apt/sources.list
RUN cat /etc/apt/sources.list
RUN apt-get clean
RUN apt-get -y update --fix-missing

```

- RUN 执行命令

`RUN` 指令是用来执行命令行命令的。由于命令行的强大能力，`RUN` 指令在定制镜像时是最常用的指令之一。

权限:为避免每一次都要加上sudo，执行下列命令：

```bash
sudo chmod 666 /var/run/docker.sock
```

## Nvidia-docker

https://github.com/NVIDIA/nvidia-docker#quickstart

### 安装

条件：安装了NVIDIA driver 和Docker（可以不用安装cuda）

```bash
nvidia-smi # 检查driver
docker version #检查docker
```

## 运行

```bash
nvidia-docker run -v $FLINGBOT_PATH:/workspace/flingbot -v /home/ylb/anaconda3/:/home/ylb/anaconda3 --gpus all --shm-size=2gb  -d -e DISPLAY=$DISPLAY -e QT_X11_NO_MITSHM=1 -it flingbot:latest
```



## TODO list

- [x] set up [Blender](https://www.blender.org/download/), [docker](https://docs.docker.com/engine/install/ubuntu/) and [nvidia-docker](https://github.com/NVIDIA/nvidia-docker#quickstart).
- [x]  download the evaluation datasets

