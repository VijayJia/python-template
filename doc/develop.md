# 准备环境

## docker

### 安装

```
sudo apt-get update

sudo apt-get install \
     ca-certificates \
     curl \
     gnupg \
     lsb-release

sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

apt-cache madison docker-ce

sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io docker-compose-plugin
```

### 设置权限
```
sudo service docker start

sudo groupadd docker
sudo usermod -aG docker $USER

newgrp docker # active group
```

### 开机启动
```
sudo systemctl enable docker.service

sudo systemctl enable containerd.service


sudo systemctl disable docker.service

sudo systemctl disable containerd.service
```


### 卸载
```
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-compose-plugin

sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

## Portainer

* 安装
```
#拉取镜像
docker pull portainer/portainer-ce:latest 

#启动容器
docker run -d  --name portainer -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /app/portainer_data:/data --restart always --privileged=true portainer/portainer-ce:latest
```
* 用户名：
```
admin: 123456ABcdef
```

## Git

* 安装
```
sudo apt-get install git
```

* 配置
```
用户名：
git config --global user.name “username”
邮箱
git config --global user.email “email”
```

* ssh
```
ssh-keygen -t RSA -C "邮箱"
```



## RabbitMQ
```
docker run -d --restart=always --hostname my-rabbit --name rabbit -p 15672:15672 -p 5672:5672 rabbitmq
docker exec -it 容器id /bin/bash
rabbitmq-plugins enable rabbitmq_management
```
default user name / password: guest

## celery
```
celery -A tasks worker --loglevel=INFO
```

## flower
```
 pip install flower
 celery -A tasks flower --broker=amqp://guest:guest@localhost:5672// --port=5555
```