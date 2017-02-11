---
title: 用chromebook安装git
layout: linux
---
在Chromebook上安装了Archlinux，合盖不能进入睡眠或挂起模式，不过最近用github的pages，主要是文本编辑，所以想改回ChromeOS，不过用github还是要有git比较好。


# 在Chromebook 上使用git

在网上搜索了一下，发现有个 [chromebrew](https://github.com/skycocker/chromebrew) 的包管理器


按照说明在开发者模式中的shell中输入

```
wget -q -O - https://raw.github.com/skycocker/chromebrew/master/install.sh | bash
```

不过用的是dropbox的下载，只好设置好代理后安装。

在安装过程中也已经把git安装上的了，版本比较旧是 1.8.4
