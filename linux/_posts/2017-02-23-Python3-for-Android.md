---
title: python3 for android  
date: 2017-02-23 13:11  
category: python3  
---  

python3 感觉不错，看着很多旧手机放着，想把它们弄出来用用，用写Android应用又比较麻烦，相着用python玩玩。  

# Python3 for Android


### 编译
在github上搜了下,发现[Python3 Android](https://github.com/rave-engine/python3-android)不过作者没继续维护，指向了[yan12125](https://github.com/yan12125/python3-android),

git clone下来，安装了ndk，再按说明make了一次。放到手机，发现是64位，无法运行。

仔细看了说明里有个编辑 env ，不过没找到文件。

在/pybuild下有个env.py，改为arm，重新编译后，装上可以运行，不过有报错信息。待后面再来处理。

### 警告处理
警告信息大概如下：
```
WARNING: linker: python3.7m.so: unused DT entry: type 0x6ffffffe arg 0x8a7d4
WARNING: linker: python3.7m.so:: unused DT entry: type 0x6fffffff arg 0x3
```

搜索了一下，发现是安卓5.1.1不支持，也没的找不编译处理的方法。
只在github上找到了一个[Android ELF cleaner](https://github.com/kost/android-elf-cleaner)

编译完后，将各个执行文件和/home/wells/python3-android/build/target/usr/lib/python3.7/lib-dynload/的文件都清除了 ELF。
再打开就没有警告信息了。