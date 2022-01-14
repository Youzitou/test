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

