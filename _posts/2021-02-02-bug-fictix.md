---
layout: post
title: fcitx 环境变量设置
date: 2021-02-02
categories: bug fcitx
tags: fcitx
cover: '../../../assets/img/20210202.jpg'
---

方式一

```plain
终端运行
sudo nano etc/profile

粘贴
export INPUT_METHOD=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
使用ctrl+o保存
终端运行
sudo source etc/profile
```

方式二

```plain
sudo apt install zenity
终端执行im-config 设置fcitx
注销重启
```

方式三

```plain
sudo apt install fcitx-bin
sudo cp /usr/share/fcitx/data/env_setup.sh /etc/profile.d/env_setup.sh
重启系统
```




