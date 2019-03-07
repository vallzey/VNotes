#### 语法

```
curl(选项)(参数)
```
#### 实例
###### 文件下载

> curl命令可以用来执行下载、发送各种HTTP请求，指定HTTP头部等操作。如果系统没有curl可以使用yum install curl安装，也可以下载安装。curl是将下载文件输出到stdout，将进度信息输出到stderr，不显示进度信息使用--silent选项。


```
curl URL --silent
```
> 这条命令是将下载文件输出到终端，所有下载的数据都被写入到stdout。
使用选项-O将下载的数据写入到文件，必须使用文件的绝对地址：


```
curl http://man.linuxde.net/text.iso --silent -O
```
> 选项-o将下载数据写入到指定名称的文件中，并使用--progress显示进度条：


```
curl http://man.linuxde.net/test.iso -o filename.iso --progress
######################################### 100.0%
```

###### 断点续传

> curl能够从特定的文件偏移处继续下载，它可以通过指定一个便宜量来下载部分文件：


```
curl URL/File -C 偏移量

#偏移量是以字节为单位的整数，如果让curl自动推断出正确的续传位置使用-C -：
curl -C -URL
```

###### 使用curl设置参照页字符串

> 参照页是位于HTTP头部中的一个字符串，用来表示用户是从哪个页面到达当前页面的，如果用户点击网页A中的某个连接，那么用户就会跳转到B网页，网页B头部的参照页字符串就包含网页A的URL。

> 使用--referer选项指定参照页字符串：


```
curl --referer http://www.google.com http://man.linuxde.net
```
###### 用curl设置cookies

> 使用--cookie "COKKIES"选项来指定cookie，多个cookie使用分号分隔：


```
curl http://man.linuxde.net --cookie "user=root;pass=123456"
```
> 将cookie另存为一个文件，使用--cookie-jar选项：


```
curl URL --cookie-jar cookie_file
```
###### 用curl设置用户代理字符串

> 有些网站访问会提示只能使用IE浏览器来访问，这是因为这些网站设置了检查用户代理，可以使用curl把用户代理设置为IE，这样就可以访问了。使用--user-agent或者-A选项：


```
curl URL --user-agent "Mozilla/5.0"
curl URL -A "Mozilla/5.0"
```

> 其他HTTP头部信息也可以使用curl来发送，使用-H"头部信息" 传递多个头部信息，例如：


```
curl -H "Host:man.linuxde.net" -H "accept-language:zh-cn" URL
```
###### curl的带宽控制和下载配额

> 使用--limit-rate限制curl的下载速度：


```
curl URL --limit-rate 50k
```
> 命令中用k（千字节）和m（兆字节）指定下载速度限制。

> 使用--max-filesize指定可下载的最大文件大小：


```
curl URL --max-filesize bytes
```
> 如果文件大小超出限制，命令则返回一个非0退出码，如果命令正常则返回0。

###### 用curl进行认证

> 使用curl选项 -u 可以完成HTTP或者FTP的认证，可以指定密码，也可以不指定密码在后续操作中输入密码：


```
curl -u user:pwd http://man.linuxde.net
curl -u user http://man.linuxde.net
```

> 只打印响应头部信息

> 通过-I或者-head可以只打印出HTTP头部信息：
> 

```
[root@localhost text]# curl -I http://man.linuxde.net
HTTP/1.1 200 OK
Server: nginx/1.2.5
date: Mon, 10 Dec 2012 09:24:34 GMT
Content-Type: text/html; charset=UTF-8
Connection: keep-alive
Vary: Accept-Encoding
X-Pingback: http://man.linuxde.net/xmlrpc.php
```
