##  shell_test (2017.11.10)
1. `输写格式`
```
num1=100
num2=100
if test $[num1] -eq $[num2]
then
    echo '两个数相等！'
else
    echo '两个数不相等！'
fi
```
2. `代码中的 [] 执行基本的算数运算`
```
#!/bin/bash

a=5
b=6

result=$[a+b] # 注意等号两边不能有空格
echo "result 为： $result"
```
3. `字符串测试` 
```
参数	说明
=	  等于则为真
!=	不相等则为真
-z  字符串	字符串的长度为零则为真
-n  字符串	字符串的长度不为零则为真
```
4. `文件测试`
* ![文件测试参数](https://github.com/GalenDeng/Shell/blob/master/%E6%96%87%E4%BB%B6%E6%B5%8B%E8%AF%95.png)
* 示例
```
cd /bin
if test -e ./bash
then
    echo '文件已存在!'
else
    echo '文件不存在!'
fi
```
* result
```
文件已存在!
```
5. `Shell还提供了与( -a )、或( -o )、非( ! )三个逻辑操作符用于将测试条件连接起来，其优先级为："!"最高，"-a"次之，"-o"最低`
```
cd /bin
if test -e ./notFile -o -e ./bash
then
    echo '有一个文件存在!'
else
    echo '两个文件都不存在'
fi
输出结果：
有一个文件存在!
```
## `数值测试`
![数值测试](https://github.com/GalenDeng/Shell/blob/master/%E6%95%B0%E5%80%BC%E6%B5%8B%E8%AF%95.JPG)
## `字符串测试`
![字符串测试](https://github.com/GalenDeng/Shell/blob/master/%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%B5%8B%E8%AF%95.JPG)
