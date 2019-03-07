> 这里的命令只用于OSX(苹果系统)
### Homebrew
#### Homebrew安装

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
#### Homebrew卸载

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
```

#### Homebrew常用命令列表

```bash
brew help #查看所有命令
brew search mysql #搜索
brew install mysql #安装软件
brew uninstall mysql #卸载软件
brew list #显示已经安装软件列表
brew services list #显示安装的服务
brew info mysql #查看信息，比如目前的版本，依赖，安装后注意事项等
```

#### Homebrew一般命令列表

```
brew services start mysql #启动
brew services stop mysql #停止)
brew services restart mysql #重启)
brew update #更新 Homebrew
brew outdated #列出所有安装的软件里可以升级的那些
brew upgrade #更新所有的包
brew upgrade $mysql #更新指定的包
brew cleanup # 清理所有包的旧版本
brew cleanup $mysql #清理指定包的旧版本
brew cleanup -n #查看可清理的旧版本包，不执行实际操作
which brew #查看 brew 命令的路径
brew home mysql #用浏览器打开官方主页
```
#### Homebrew锁定不想更新的包
如果经常更新的话，brew update 一次更新所有的包是非常方便的。但我们有时候会担心自动升级把一些不希望更新的包更新了。数据库就属于这一类，尤其是 PostgreSQL 跨 minor 版本升级都要迁移数据库的。我们更希望找个时间单独处理它。这时可用 brew pin 去锁定这个包，然后 brew update 就会略过它了，用到的命令如下：

```
brew pin $FORMULA #锁定某个包
brew unpin $FORMULA # 取消锁定
brew deps #查看包的依赖关系，常用它来查看已安装的包的依赖，然后判断哪些包是可以安全删除的。
brew deps --installed --tree #查看已安装的包的依赖，树形显示
```
#### Homebrew 扩展推荐(brew cask)

```
brew cask search    # 列出所有可以被安装的软件
brew cask search name   # 查找所有和 name相关的应用
brew cask install name  # 下载安装软件
brew cask uninstall name    # 卸载软件
brew cask info app  # 列出应用的信息
brew cask list  # 列出本机安装过的软件列表
brew cask cleanup   # 清除下载的缓存以及各种链接信息
brew cask uninstall name && brew cask install name    ＃更新程序 （目前homebrew-cask 并没有命令直接更新已安装的软件，软件更新主要是通过软件自身的完成更新）
```
#### Homebrew 扩展推荐([brew-cask-upgrade](https://github.com/buo/homebrew-cask-upgrade))
```
brew cu #更新brew cask
```