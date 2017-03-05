---
title: python ntp
date: 2017-03-04 23:10
---

手机上的定位总是感觉时间同步很差，以前试过14颗星了，还是定不了位，感觉像是ntp问题，网上搜索了是改cn.pool.ntp.org，不过感觉依然很差。想差能不能用python同步一下。

# python ntp 同步时间

在百度搜了一下代码是这样


```python
import os 
import time 
import ntplib 
c = ntplib.NTPClient() 
response = c.request('pool.ntp.org') 
ts = response.tx_time 
_date = time.strftime('%Y-%m-%d',time.localtime(ts)) 
_time = time.strftime('%X',time.localtime(ts)) 
os.system('date {} && time {}'.format(_date,_time)) 
```

在安卓上试了一下，在c.request那里报错了。查了一下是需要在/etc/services加什么内容指定端口，不过没具体。查了一下c.request是可以直接指定的，查了ntp是123，
```
c = c.request('pool.ntp.org',port=123)
```

不过在设置时间时又错了。本来应该这样的，不过可能是手机问题还是不可以。
```
os.system('date -s "{} {}"'.format(_date,_time))
```
最后看了busybox date是可以的就

```
os.system('busybox date -s "{} {}"'.format(_date,_time))
```


可以设置了，不过是间又提前了8个小时（跟时区对应），应该是localtime的问题，查了下应该改为 gmtime

```
_date = time.strftime('%Y-%m-%d',time.gmtime(ts)) 
_time = time.strftime('%X',time.gmtime(ts))
```











