### Ubuntu桌面快捷

##### 位置

```
cd /usr/share/applications
```

##### 使用gedit创建文件

```
sudo gedit navicat.desktop
```

##### 文件格式

- 例子1

```
[Desktop Entry]
Encoding=UTF-8
Name=Navicat
Comment=Navicat Premium
Exec=/opt/Navicat/start_navicat
Icon=/opt/Navicat/navicat.png
Terminal=false
StartupNotify=true
Type=Application
Categories=Application;Development;
```
- 例子2

```
[Desktop Entry]
Encoding=UTF-8
Version=1.0
Type=Application
Terminal=false
Name=Telegram Desktop
Exec=/opt/telegram/Telegram -- %u
Comment=Official desktop version of Telegram messaging app
Icon=/opt/telegram/telegram.svg
StartupWMClass=Telegram
Categories=GNOME;GTK;Network;
MimeType=application/x-xdg-protocol-tg;x-scheme-handler/tg;
X-Desktop-File-Install-Version=0.22
```