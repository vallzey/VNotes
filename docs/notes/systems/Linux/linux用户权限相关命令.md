### Ubuntu

##### useradd
```bash
useradd -r -m -s /bin/bash vallzey
passwd spark
chmod +w /etc/sudoers
```

##### 查看目录或文件权限
```bash
getfacl 目录或文件
```

##### 设置目录或文件权限
```bash
sudo setfacl -m user:vallzey:rwx test
```

##### chown
> 利用 chown命令 可以将文件的拥有者加以改变。

- -R处理指定目录以及其子目录下的所有文件

```
sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
sudo chmod g+rwx "$HOME/.docker" -R
```


##### 创建一个用户组
```bash
sudo groupadd docker
```

##### 添加一个用户在到存在的用户组中
> 生效需要注销重新登录

```bash
sudo usermod -aG docker $USER
```












