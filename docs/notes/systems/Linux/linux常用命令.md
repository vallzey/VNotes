### Ubuntu下的一些命令

##### display service(显示服务)
```bash
# Temporarily turn off the display service
sudo service lightdm stop
# turn on the display service
sudo service lightdm start
```

##### use 'curl' send a post request
```bash
# post
curl -d "opr=pwdLogin&userName=171050050&pwd=0050131579&rememberPwd=1" "http://2.2.2.2/ac_portal/login.php"

# check dns
cat /etc/resolv.conf
```


##### 获取文件中的部分
- 获取user-item.lst文件的5-10行,复制到test文件中
```bash
sed -n '5,10p' user-item.lst > test
```
- 获取user-item.lst文件的前100行,复制到test文件中
```bash
head -100 user-item.lst > test
```
- 获取user-item.lst文件的后100行,复制到test文件中
```bash
tail -20 user-item.lst > test
```


##### Configuring remote access with systemd unit file
1. open an override file for docker.service in a text editor.
```bash
$ sudo systemctl edit docker.service
```
2. Add or modify the following lines, substituting your own values.
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://127.0.0.1:2375
```
3. Save the file.
4. Reload the systemctl configuration.
```bash
$ sudo systemctl daemon-reload
```
5. Restart Docker.
```bash
$ sudo systemctl restart docker.service
```

##### systemd 设置开机自动启动
```bash
sudo systemctl enable docker
sudo systemctl disable docker
```

##### watch间隔1秒刷新
```bash
watch -n 1 -d nvidia-smi
watch -n 1 -d 'ps aux | grep mysql'
```

##### 添加和删除变量
```bash
# 添加http代理
export http_proxy=127.0.0.1:1080
# 删除http代理
unset http_proxy
```

##### 更换编译器
```bash
sudo apt install gcc-6 g++-6
sudo ln -s /usr/bin/gcc-6 /usr/local/bin/gcc
sudo ln -s /usr/bin/g++-6 /usr/local/bin/g++
```

##### 查看和杀死被锁进程
```bash
sudo lsof /var/lib/dpkg/lock-frontend
sudo kill -9 10963
```

##### 创建文件
```bash
touch test
```

##### 查看端口
```bash
sudo netstat -npltu | grep 21
```


##### 解压zip
- -O    以指定的字符集显示和解压文件
- -d    到指定的目录
```bash
unzip -O CP936 day01.zip -d ./day01/
```

##### 解压rar
- x     解压
```bash
unrar x day01.rar
```

##### 查看应用的进程树
```bash
pstree -ap|grep gunicorn
```

##### 设置快捷方式
> 可以理解为从 sites-available/ 目录下发送了一个配置文件的快捷方式到 sites-enabled/ 目录。

```bash
sudo ln -s /etc/nginx/sites-available/demo.zmrenwu.com /etc/nginx/sites-enabled/demo.zmrenwu.com
```

##### 开启gunicom
```bash
gunicorn --bind unix:/tmp/myweb.socket VItest.wsgi:application
```

##### Git 的操作

> 重置想要上传到github的文件

```bash
git reset HEAD <file>
```

> 获取当前git项目的状态

```bash
git status
```

> 添加所有的未添加的文件到github上

```bash
git add -A
```

> commit, 并添加本次commit的说明

```bash
git commit -m "备注说明"
```

> 上传到原始的master分支

```bash
git push -u origin master
```

> 创建一个叫做"feature_x"的分支，并切换过去：

```bash
git checkout -b feature_x
```

> 切换回主分支：

```bash
git checkout master
```

> 把新建的分支删掉：

```bash
git branch -d feature_x
```

> 要更新你的本地仓库至最新改动:

```bash
git pull
```

> 要合并其他分支到你的当前分支（例如 master）

```bash
git merge <branch>
```

> 在合并改动之前，你可以使用如下命令预览差异

```bash
git diff <source_branch> <target_branch>
```

##### 删除软件(如:ngin)
- –purge    包括配置文件
```bash
sudo apt-get --purge remove nginx
```

##### 罗列出相关的软件(比如:与nginx相关的软件)
- –purge    包括配置文件
```bash
dpkg --get-selections|grep nginx
```

##### kill (比如:nginx进程)

```bash
sudo kill  -9  7875 7876 7877 7879
```

##### 全局查找(比如:nginx相关的文件)
```bash
sudo  find  /  -name  nginx*
```

##### 将 alias lg ='lazygit' 写入.zshrc中,可以通过使用lg代替lazygit
```bash
echo “alias lg ='lazygit'”>>〜/.zshrc
```