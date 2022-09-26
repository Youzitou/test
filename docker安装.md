# docker安装


```shell
# 安装docker前准备  centos7 及以上版本 64位 linux 内核3.8以上版本
sudo yum -y install gcc
sudo yum -y install gcc-c++
sudo yum install -y  yum-utils
```

```shell
# 设置镜像仓库地址
sudo yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

![1642172008142](E:\GitHubProject\test\img\1642172008142.png)

```shell
# 将软件包信息提前在本地索引缓存
yum makecache fast  #或yum makecache timer
```

![1642172112721](E:\GitHubProject\test\img\1642172112721.png)

```shell
# 安装docker引擎
sudo yum install docker-ce docker-ce-cli containerd.io 
```

```shell
# 查看是否安装安装
yum list installed | grep docker
```

![1642172257310](E:\GitHubProject\test\img\1642172257310.png)

```shell
# 查看docker版本
docker version
```

![1642172308036](E:\GitHubProject\test\img\1642172308036.png)

```shell
# 启动 docker
sudo systemctl start docker
```

```shell
# 查看是否启动成功
ps -ef | grep docker
```

![1642172372118](E:\GitHubProject\test\img\1642172372118.png)

```shell
# 运行docker  出现如下运行成功
sudo docker run hello-world
```

![1642172840638](E:\GitHubProject\test\img\1642172840638.png)

```shell
# 配置镜像加速器  阿里云->弹性计算->容器计算服务->镜像加速器
sudo mkdir -p /etc/docker
# 切换到该目录
cd /etc/docker/
#  执行以下
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://1m37o0c0.mirror.aliyuncs.com"]
}
EOF
```

![1642174195329](C:\Users\liuyouyun\AppData\Roaming\Typora\typora-user-images\1642174195329.png)

```shell
# 重启
sudo systemctl daemon-reload
sudo systemctl restart docker
# 再次运行docker ，可以看到运行成功
sudo docker run hello-world
```

# docker常用命令

帮助启动类命令

镜像命令

容器命令