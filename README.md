# 0 本仓库参考（致谢）

https://github.com/PaoPaoRobot/docker-ubuntu-xfce-vnc-desktop





# 1 构建



```shell
# -t 指定你的镜像名字，在构建之前可以提前拉取相应的ubuntu基础镜像
cd My_DockerBuild/melodic_vnc_ssh
# docker pull osrf/ros:melodic-desktop-full
docker build -t my_melodic_vnc .
```

在vnc输入 `IP_docker:5900`即可进入









#  :star: 下面的是原作者的README



ubuntu-xfce-vnc
=========================

## Features
- VNC server
- SSH

## Pull from dockerhub

```
$ docker pull paopaorobot/ubuntu-xfce-vnc
```

## Build yourself

```
$ git clone https://github.com/PaoPaoRobot/docker-ubuntu-xfce-vnc-desktop.git
$ docker build --rm -t paopaorobot/ubuntu-xfce-vnc docker-ubuntu-xfce-vnc-desktop
```

## Run

### Use it headless
```
$ docker run -it paopaorobot/ubuntu-xfce-vnc
```
Now you can use the command line

### Use it with ssh
```
$ docker run -it -p [port]:22 paopaorobot/ubuntu-xfce-vnc
```
You will see the random password in terminal. You can use it to login ssh by
```
$  ssh -o 'UserKnownHostsFile=/dev/null' root@localhost -p [port]
```
> 注意：
>
> 如果你不使用`-o 'UserKnownHostsFile=/dev/null'`这个参数的话，当你换镜像去连接的时候可能会报错
>
> 相当于使用 黑洞 `/dev/null`去保存k值，就不会报错

If you want to set password by yourself, you can run 

```
$ docker run -it -p [port]:22 -e SSHPW=[YOUR_PW] paopaorobot/ubuntu-xfce-vnc
```

You need to set the port, e.g. `2222`. 

### Use it with vnc
```
$ docker run -i -t -p 5900:5900 paopaorobot/ubuntu-xfce-vnc
```
if you want to set resolution
```
$ docker run -i -t -p 5900:5900 -e RESOLUTION=1920x1080 paopaorobot/ubuntu-xfce-vnc
```

Then open vnc viewer and input `<YOUR IP>:5900`, and you can use the desktop by vnc. If you run the image on your own pc, you can only input `:5900` in vnc viewer.

### Use random port
If you don't want to set port by yourself, you can use random port with `-P` param. e.g.
```
$ docker run -it -P paopaorobot/ubuntu-xfce-vnc
```
Now, you need `docker port` to find out the ports
```
$ docker port [container_id] [port]
```
When [port] is `22`, you get the port for ssh. When [port] is `5900`, you get the port for vnc viewer.

## Trobleshooting
You can find logs under /var/log/ in container.

