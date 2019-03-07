### 安装
##### 在ubuntu 16.04上安装
```bash
# Uninstall old version
$ sudo apt-get install supervisor
```
### config

> Supervisor 是一个 C/S 模型的程序，supervisord 是 server 端，supervisorctl 是 client 端。
#### supervisord

###### 下面介绍 supervisord 配置方法。supervisord 的配置文件默认位于 /etc/supervisord.conf，内容如下（;后面为注释）：

```
; supervisor config file

[unix_http_server]
file=/var/run/supervisor.sock   ; (the path to the socket file) UNIX socket 文件，supervisorctl 会使用
chmod=0700                       ; sockef file mode (default 0700) socket 文件的 mode，默认是 0700

[supervisord]
logfile=/var/log/supervisor/supervisord.log ; (main log file;default $CWD/supervisord.log) 日志文件，默认是 $CWD/supervisord.log
pidfile=/var/run/supervisord.pid ; (supervisord pidfile;default supervisord.pid) pid 文件
childlogdir=/var/log/supervisor            ; ('AUTO' child log dir, default $TEMP)

; the below section must remain in the config file for RPC
; (supervisorctl/web interface) to work, additional interfaces may be
; added by defining them in separate rpcinterface: sections
[rpcinterface:supervisor]
supervisor.rpcinterface_factory = supervisor.rpcinterface:make_main_rpcinterface

[supervisorctl]
serverurl=unix:///var/run/supervisor.sock ; use a unix:// URL  for a unix socket 通过 UNIX socket 连接 supervisord，路径与 unix_http_server 部分的 file 一致

; 在增添需要管理的进程的配置文件时，推荐写到 `/etc/supervisor/conf.d/` 目录下，所以 `include` 项，就需要像如下配置。
; 包含其他的配置文件
[include]
files = /etc/supervisor/conf.d/*.conf ; 引入 `/etc/supervisor/conf.d/` 下的 `.conf` 文件
```
##### program 配置

###### program 的配置文件就写在，supervisord 配置中 include 项的路径下：/etc/supervisor/conf.d/，然后 program 的配置文件命名规则推荐：app_name.conf

```
[program:app] ; 程序名称，在 supervisorctl 中通过这个值来对程序进行一系列的操作
autorestart=True      ; 程序异常退出后自动重启
autostart=True        ; 在 supervisord 启动的时候也自动启动
redirect_stderr=True  ; 把 stderr 重定向到 stdout，默认 false
environment=PATH="/home/app_env/bin"  ; 可以通过 environment 来添加需要的环境变量，一种常见的用法是使用指定的 virtualenv 环境
command=python server.py  ; 启动命令，与手动在命令行启动的命令是一样的
user=ubuntu           ; 用哪个用户启动
directory=/home/app/  ; 程序的启动目录
stdout_logfile_maxbytes = 20MB  ; stdout 日志文件大小，默认 50MB
stdout_logfile_backups = 20     ; stdout 日志文件备份数
; stdout 日志文件，需要注意当指定目录不存在时无法正常启动，所以需要手动创建目录（supervisord 会自动创建日志文件）
stdout_logfile = /data/logs/usercenter_stdout.log
```

### supervisorctl 操作

```
# 使用命令进入supervisor进入客户端
sudo supervisorctl
# 重读配置文件
sudo supervisorctl reread
# 更新
sudo supervisorctl update
```
##### 在supervisor客户端中:
- help # 查看帮助
- status # 查看程序状态
- stop program_name # 关闭 指定的程序
- start program_name # 启动 指定的程序
- restart program_name # 重启 指定的程序
- tail -f program_name # 查看 该程序的日志

