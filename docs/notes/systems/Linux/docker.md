
### 安装
##### 在ubuntu 16.04上安装
```bash
# Uninstall old version
$ sudo apt-get remove docker docker-engine docker.io

# Update the apt package index
$ sudo apt-get update

# Install packages to allow apt to use a repository over HTTPS
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
    
# Add Docker’s official GPG key
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88,
# by searching for the last 8 characters of the fingerprint.
$ sudo apt-key fingerprint 0EBFCD88

# Use the following command to set up the stable repository.
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

# Update the apt package index.
$ sudo apt-get update

#Install the latest version of Docker CE, or go to the next step to install a specific version
$ sudo apt-get install docker-ce
```
##### 列出可用版本,并且下载
```bash
# List the versions available in your repo
$ apt-cache madison docker-ce

# Install a specific version by its fully qualified package name, which is package name (docker-ce) “=” version string (2nd column)
$ sudo apt-get install docker-ce=<VERSION>

# Verify that Docker CE is installed correctly by running the hello-world image.
$ sudo docker run hello-world
```

### 常用命令

```bash
## List Docker CLI commands
docker
docker container --help

## Display Docker version and info
docker --version
docker version
docker info

## Execute Docker image
docker run hello-world

## List Docker images
docker image ls

## List Docker containers (running, all, all in quiet mode)
docker container ls
docker container ls --all
docker container ls -aq
```

### Containers

##### 为您的环境提供快速测试运行，以确保您完成所有设置
```
docker run hello-world
```
##### 在docker中,这些便携的镜像是由Dockerfile定义
**example**
> 以下三个文件需要放在同一个文件夹
```
# Dockerfile
# Use an official Python runtime as a parent image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```
```
# 其中requirements.txt是python的依赖文件的包
Flask
Redis
```
```
# app.py
from flask import Flask
from redis import Redis, RedisError
import os
import socket

# Connect to Redis
redis = Redis(host="redis", db=0, socket_connect_timeout=2, socket_timeout=2)

app = Flask(__name__)

@app.route("/")
def hello():
    try:
        visits = redis.incr("counter")
    except RedisError:
        visits = "<i>cannot connect to Redis, counter disabled</i>"

    html = "<h3>Hello {name}!</h3>" \
           "<b>Hostname:</b> {hostname}<br/>" \
           "<b>Visits:</b> {visits}"
    return html.format(name=os.getenv("NAME", "world"), hostname=socket.gethostname(), visits=visits)

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

> 上面的例子,由于没有docker中没有安装redis本身,所以所以会如期的一样报错,但是也足以作为一个例子使用

##### Build the app
1. 使用上面的例子构建一个app,先查看当前目录的文件
```
$ ls
Dockerfile		app.py			requirements.txt
```
2. 使用命令构建app
```
docker build -t friendlyhello .
```
3. 查看docker的镜像
```
$ docker image ls

REPOSITORY            TAG                 IMAGE ID
friendlyhello         latest              326387cea398
```

##### Run the app
运行应用程序，使用-p将计算机的端口4000映射到容器的已发布端口80
```
docker run -p 4000:80 friendlyhello
```
使用 **curl** 测试
```
$ curl http://localhost:4000

<h3>Hello World!</h3><b>Hostname:</b> 8fc990912a14<br/><b>Visits:</b> <i>cannot connect to Redis, counter disabled</i>
```
现在让我们以分离模式在后台运行应用程序：
```
docker run -d -p 4000:80 friendlyhello
```
使用docker container stop来结束进程，使用CONTAINER ID:
```
docker container stop 1fa4ab2cf395
```

##### Share your image
###### Log in with your Docker ID
```
$ docker login
```
###### Tag the image
```
# 将某一个镜像放在某个用户的repository下面,并且打上标签
docker tag image username/repository:tag
```
```
# For example:
# 添加标签
docker tag friendlyhello vallzey/get-started:part2
# 去除标签
docker image rm vallzey/get-started:part2
```
###### Publish the image
```
docker push username/repository:tag
```
```
# For example:
docker push vallzey/get-started:part2
```
现在可以在任何机上运行这个image,如果本地没有的话,系统就会从网上下载
```
docker run -p 4000:80 username/repository:tag
```
##### 常用命令
```
docker build -t friendlyhello .  # Create image using this directory's Dockerfile
docker run -p 4000:80 friendlyhello  # Run "friendlyname" mapping port 4000 to 80
docker run -d -p 4000:80 friendlyhello         # Same thing, but in detached mode
docker container ls                                # List all running containers
docker container ls -a             # List all containers, even those not running
docker container stop <hash>           # Gracefully stop the specified container
docker container kill <hash>         # Force shutdown of the specified container
docker container rm <hash>        # Remove specified container from this machine
docker container rm $(docker container ls -a -q)         # Remove all containers
docker image ls -a                             # List all images on this machine
docker image rm <image id>            # Remove specified image from this machine
docker image rm $(docker image ls -a -q)   # Remove all images from this machine
docker login             # Log in this CLI session using your Docker credentials
docker tag <image> username/repository:tag  # Tag <image> for upload to registry
docker push username/repository:tag            # Upload tagged image to registry
docker run username/repository:tag                   # Run image from a registry
```













