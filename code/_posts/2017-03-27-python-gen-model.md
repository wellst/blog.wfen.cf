---
title:  通过python 读取mysql 生成model dal
date: 2017-03-27 22:30
category: python3
---
# 通过python 读取mysql 生成model dal
因为最近用java写点东西，而有很多Model,Dal要写，只好用Python生成一些常用的代码。

因为框架是同事弄的，所以只好自己写。

## 读取数据表的设计

读取表格名称  

```python
sql ="SELECT table_name FROM `TABLES` WHERE table_schema='%s'"%(dbname)
```

读取表格设计  

```python
tblsql="SELECT column_name,data_type,column_key,IFNULL(column_comment,'') column_comment,IFNULL(extra,'') extra,IFNULL(column_default,'') column_default FROM information_schema.columns WHERE table_schema ='%s'  AND table_name ='%s' "%(dbname,tbl)
```
为了更好的生成代码，都加了注释，用于生成表的label

- col_key='PRI' 应该是主键  
- col_key='MUL' 应该是外键  
- col_key='UNI' 应该是唯一 

extra
- 'auto_increment' 为自增加，一般用在id
- 'on update CURRENT_TIMESTAMP' 更新时间戳，一般用在记录更新时间

default
- 'CURRENT_TIMESTAMP' 添加时间
- 0 bit默认False int 则默认为0

fieldtype
自己常用的类型
- bigint -> Long
- varchar -> String
- timestamp,datetime -> Timestamp
- time -> Time
- date -> Date
- int -> Integer
- bit -> Boolean

```python
def conv_type(data_type):
    if(data_type=='bigint'):
        return 'Long';
    elif (data_type=='varchar'):
        return 'String'
    elif (data_type=='timestamp'):
        return 'Timestamp'
    elif (data_type=='datetime'):
        return 'Timestamp'
    elif (data_type=='time'):
        return 'Time'
    elif (data_type=='date'):
        return 'Date'
    elif (data_type=='int'):
        return 'Integer'
    elif (data_type=='bit'):
        return 'Boolean'
```

### 生成表主要的描述类
```python
def __init__(self, tblname, rows):
        self.Classname = tblname.capitalize()#类名首字母大写
        self.modelname = tblname #实例名全小写
        self.Fields = [] #字段
        self.Keyfield = {} #主键 用在get del update
        self.UniFields = [] #唯一 用于getbyField
        self.implines = '' #import行，主要是Date,Time,Timestamp
        self.imp1 = ''
        self.imp2 = ''
        self.imp3 = ''
        self.Idfield = {} #外键用在select控件的value
        self.Namefield = {} #外键用在select的text
        for r in rows:
            ftype = conv_type(r[1])
            if ftype == 'Date':
                self.imp1 = 'import java.sql.Date;\n'
            if ftype == 'Time':
                self.imp2 = 'import java.sql.Time;\n'
            if ftype == 'Timestamp':
                self.imp3 = 'import java.sql.Timestamp;\n'
            nfield = {'Field':r[0].capitalize(),
                'fieldname': r[0],
                'fieldtype': ftype,
                'extra': r[4],
                'default': r[5],
                'comment': r[3],
                'col_key': r[2]}
            self.Fields.append(nfield)
            if r[2] == 'PRI':
                self.Keyfield = nfield
            if r[2] == 'UNI':
                self.UniFields.append(nfield)
            if nfield['fieldname'] == 'name':
                self.Namefield = nfield
            if nfield['fieldname'] == 'id':
                self.Idfield = nfield
        if self.Idfield == {}:
            self.Idfield = self.Namefield
        self.implines = self.imp1 + self.imp2 + self.imp3
```


