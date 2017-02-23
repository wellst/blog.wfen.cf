---
title: python3 for Android  
date: 2017-02-23 13:11  
category: python3  
---  

python3 感觉不错，看着很多旧手机放着，想把它们弄出来用用，用写Android应用又比较麻烦，相着用python玩玩。  

＃ Python3 for Android

在github上搜了下,发现[Python3 Android](https://github.com/rave-engine/python3-android)不过作者没继续维护，指向了[yan12125](https://github.com/yan12125/python3-android),

git clone下来，安装了ndk，再按说明make了一次。放到手机，发现是64位，原来说明里有个编辑 env ，不过没找到文件，这次失败后，再仔细看了各个文件，发现在/pybuild下有个env.py，改为arm，重新编译后，装上可以运行，不过有报错信息。待后面再来处理。