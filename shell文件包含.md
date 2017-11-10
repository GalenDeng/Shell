## shell文件包含 (2017.11.10)
* Shell也可以包含外部脚本。这样可以很方便的封装一些公用的代码作为一个独立的文件
1. `Shell文件包含的语法格式`
```
. filename   # 注意点号(.)和文件名中间有一空格
OR
source filename
```
2. `实例`
* 1) test1.sh
```
#!/bin/bash
url="http://www.runoob.com"
```
* 2) test2.sh
```
#!/bin/bash
#使用 . 号来引用test1.sh 文件
. ./test1.sh

# 或者使用以下包含文件代码
# source ./test1.sh
echo "菜鸟教程官网地址：$url"
```
* 3) test2.sh 添加可执行权限并执行
```
$ chmod +x test2.sh 
$ ./test2.sh 

* 被包含的文件 test1.sh 不需要可执行权限
```