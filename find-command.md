> 
-name pattern：按文件名查找，支持使用通配符 * 和 ?.     
-type type：按文件类型查找，可以是 f（普通文件）、d（目录）、l（符号链接）等        
-size [+-]size[cwbkMG]：按文件大小查找，支持使用 + 或 - 表示大于或小于指定大小，单位可以是 c（字节）、w（字数）、b（块数）、k（KB）、M（MB）或 G（GB）。         
-mtime days：按修改时间查找，支持使用 + 或 - 表示在指定天数前或后，days 是一个整数表示天数。
-user username：按文件所有者查找。    
-group groupname：按文件所属组查找。        


1. find . -type f

```
$ find . -type f -name file1.txt
./app/file1.txt
./file1.txt
```

名称支持通配符，但是必须用双引号包括：
```
$ find . -name "file*"
./app/file1.txt
./app/file2.txt
./file1.txt
./file2.txt

```

在 name 前添加一个 i —— -iname，表示忽略大小写：
```
$ find .-iname "*.js"
```

删除查找的结果(或者用 -exec commmand {} \; )

可以使用 -delete 用来删除查找的结果，例如删除当前仓库中所有的 html 文件：
```
$ find . -name "*.html" -type f -delete
```

Reference link:
- https://pengfeixc.com/blogs/developer-handbook/linux-find-command
- https://www.runoob.com/linux/linux-comm-find.html