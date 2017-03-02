---
title: ChromeBook安装Git
date: 2017-03-02 23:00
category: linux
---

之前用chromebrew 的包安装了git 是1.8.4。今天被娃把电脑恢复了验证，原来的东西都没了。只好重新来。
在装了python和git的其他依赖后，去archlinux上看了git 2.12.0只是多了个openssl.再看了chromebrew的包是要编译的。就切换到archlinux，下了1.10的，编译完，发现在编译git的时候提示出错，只好卸载后重新下了个1.02的，这次git也一起编译成功，回到chromeos把archlinux系统的/usr/local/下的东西都复制到ChromeOS里。试了一下 git 好像还正常。后面继续用用再说。