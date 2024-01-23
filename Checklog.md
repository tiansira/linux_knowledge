# 1. tail
```
tail -f file.log 循环读取

eg:
tail -n 10 test.log   查询日志尾部的最后10行
tail -n +10 test.log  查询10行之后的所有行
tail -fn 10 test.log  循环实时查看最后10行记录

一般一会配合grep使用:
tail -fn 1000 test.log | grep '关键字'

```

# 2. head
跟tail相反的head是看前多少行

head -n 10 test.log 查询日志文件中的前10行日志.
head -n -10 test.log  查询日志文件除了最后10行的其他所有日志.

# 3. less

/字符串：向下搜索"字符串"的功能   
?字符串：向上搜索"字符串"的功能   
n：重复前一个搜索（与 / 或 ? 有关).  
N：反向重复前一个搜索（与 / 或 ? 有关).   
b 向后翻一页