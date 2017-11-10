## shell输入输出重定向 （2017.11.10）
1. `基本操作` 
```
command > file	将输出重定向到 file。
command < file	将输入重定向到 file。
command >> file	将输出以追加的方式重定向到 file。
n > file	      将文件描述符为 n 的文件重定向到 file。
n >> file	      将文件描述符为 n 的文件以追加的方式重定向到 file。
n >& m	        将输出文件 m 和 n 合并。
n <& m	        将输入文件 m 和 n 合并。
<< tag	        将开始标记 tag 和结束标记 tag 之间的内容作为输入。
```
2. `将 stdout 和 stderr 合并后重定向到 file`
```
$ command > file 2>&1
OR
$ command >> file 2>&1
```
3. `对 stdin 和 stdout 都重定向`
```
$ command < file1 >file2
```
4. `Here Document 是 Shell 中的一种特殊的重定向方式，用来将输入重定向到一个交互式 Shell 脚本或程序`
```
command << delimiter
    document
delimiter
它的作用是将两个 delimiter 之间的内容(document) 作为输入传递给 command。
注意：
结尾的delimiter 一定要顶格写，前面不能有任何字符，后面也不能有任何字符，包括空格和 tab 缩进。
开始的delimiter前后的空格会被忽略掉。
```
5. `/dev/null`
```
/dev/null 是一个特殊的文件，写入到它的内容都会被丢弃；如果尝试从该文件读取内容，那么什么也读不到。
但是 /dev/null 文件非常有用，将命令的输出重定向到它，会起到"禁止输出"的效果
```
6. `希望屏蔽 stdout 和 stderr，可以这样写`
```
$ command > /dev/null 2>&1
```
7. `&意义`
```
这里的&没有固定的意思
放在>后面的&，表示重定向的目标不是一个文件，而是一个文件描述符
```
```
换言之 2>1 代表将stderr重定向到当前路径下文件名为1的regular file中，而2>&1代表将stderr重定向到文件描述符为1的文件(即/dev/stdout)中，这个文件就是stdout在file system中的映射
```
* &>file是一种特殊的用法，也可以写成>&file
* &>或者>&视作整体，分开没有单独的含义
```
* 两者都相当于  >file 2>&1
```