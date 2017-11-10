## shell介绍 （2017.11.09）
1. `在一般情况下，人们并不区分 Bourne Shell 和 Bourne Again Shell，所以，像 #!/bin/sh，它同样也可以改为 #!/bin/bash`
* #! 告诉系统其后路径所指定的程序即是解释此脚本文件的 Shell 程序

[运算符章节](http://www.runoob.com/linux/linux-shell-basic-operators.html)
[Shell教程](http://www.runoob.com/linux/linux-shell.html)

2. `执行脚本的方法`
* 作为可执行程序执行
```
chmod +x ./test.sh  #使脚本具有执行权限
./test.sh  #执行脚本
```
* 作为解释器参数
```
/bin/sh test.sh
/bin/php test.php
```
3. `Shell变量`
```
 定义变量时，变量名不加美元符号（$，PHP语言中变量需要）
```
4. `将/etc下的目录的文件名循环`
```
* for file in `ls /etc`
```
5. `使用变量`
```
your_name="qinjx"
echo $your_name
```
6. `推荐给所有变量加上花括号，这是个好的编程习惯`
```
for skill in Ada Coffe Action Java; do
    echo "I am good at ${skill}Script"
done
```
```
如果不给skill变量加花括号，写成echo "I am good at $skillScript"，解释器就会把$skillScript当成一个变量（其值为空），代码执行结果就不是我们期望的样子了。
```
7. `只读变量`
```
galen@galen-virtual:~$ cat var_name 
#!/bin/bash
myURL="W3C"
readonly myUrl
myUrl="http://www"
```
* result
```
galen@galen-virtual:~$ /bin/sh var_name
var_name: 4: var_name: myUrl: is read only
galen@galen-virtual:~$ chmod a+x var_name 
galen@galen-virtual:~$ /bin/sh var_name
var_name: 4: var_name: myUrl: is read only
```
8. `显示目录下的文件的脚本编写示例`
```
galen@galen-virtual:~$ cat see.sh 
#!/bin/sh
for file in `ls /etc`;do
        echo "${file}"
done
```
* chomd a+x see.sh 
* ./see.sh
* 注意： 不给file变量加花括号的话，解释器会把$file当成一个变量(其值为空)
* 赋值的时候不能写$your_name="alibaba"，使用变量的时候才加美元符（$）
9. `删除变量`
```
unset 命令可以删除变量
```
10. `字符串的写法建议用双引号`
```
your_name="qinjx"
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting $greeting_1
```
11. `获取字符串个数`
```
galen@galen-virtual:~$ string="abaa"
galen@galen-virtual:~$ echo ${#string}
4
```
12. `提取子字符串`
```
galen@galen-virtual:~$ echo ${string:1:4}
baa
```
13. `查找子字符串`
```
galen@galen-virtual:~$ string="runoob is a great company"
galen@galen-virtual:~$ echo `expr index "$string" is`
8
galen@galen-virtual:~$ echo `expr index "$string" a`
11
```
14. `shell中定义数组`
```
在Shell中，用括号来表示数组，数组元素用"空格"符号分割开。定义数组的一般形式为：
数组名=(值1 值2 ... 值n)
```
```
array_name=(value0 value1 value2 value3)
```
* or
```
array_name=(
value0
value1
value2
value3
)
```
* or
```
还可以单独定义数组的各个分量：
array_name[0]=value0
array_name[1]=value1
array_name[n]=valuen
```
15. `读取数组`
* 法一：
```
* ${数组名[下标]}
* example  valuen=${array_name[n]}
```
* 法二：用@符号可以获取数组中的所有元素
```
echo ${array_name[@]}
```
* result
```
galen@galen-virtual:~$ array_val=(val1 val2 val3 val4)
galen@galen-virtual:~$ echo ${array_val[@]}
val1 val2 val3 val4
```
16. `Shell注释`
* 以"#"开头的行就是注释，会被解释器忽略
* sh里没有多行注释
* 技巧
```
如果在开发过程中，遇到大段的代码需要临时注释起来，过一会儿又取消注释，怎么办呢？
每一行加个#符号太费力了，可以把这一段要注释的代码用一对花括号括起来，定义成一个函数，没有地方调用
这个函数，这块代码就不会执行，达到了和注释一样的效果。
```
17. shell中的 `# ## % %%`
```
#、## 表示从左边开始删除。一个 # 表示从左边删除到第一个指定的字符；
两个 # 表示从左边删除到最后一个指定的字符
%、%% 表示从右边开始删除。一个 % 表示从右边删除到第一个指定的字符；
两个 % 表示从左边删除到最后一个指定的字符
删除包括了指定的字符本身。
```
18. `shell传递参数`
* 我们可以在执行 Shell 脚本时，向脚本传递参数，脚本内获取参数的格式为：$n。n 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推……
* 而$0 为执行的文件名
```
galen@galen-virtual:~$ cat shell_para.sh 
#!/bin/sh
echo "$0"
echo "$1"
echo "$2"
echo "${3}"
```
```
galen@galen-virtual:~$ ./shell_para.sh 1 2 3
./shell_para.sh
1
2
3
```
19. `$* 与 $@ 区别`
```
相同点：都是引用所有参数。
不同点：只有在双引号中体现出来。假设在脚本运行时写了三个参数 1、2、3，，则 " * " 等价于 "1 2 3"（传递了一个参数），而 "@" 等价于 "1" "2" "3"（传递了三个参数）。
```
```
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

echo "-- \$* 演示 ---"
for i in "$*"; do
    echo $i
done

echo "-- \$@ 演示 ---"
for i in "$@"; do
    echo $i
done
执行脚本，输出结果如下所示：
$ chmod +x test.sh 
$ ./test.sh 1 2 3
-- $* 演示 ---
1 2 3
-- $@ 演示 ---
1
2
3
```
20. `特殊字符表`
![特殊字符]()
21. `Shell数组`
* 数组中可以存放多个值。Bash Shell 只支持一维数组 初始化时不需要定义数组大小
* 读取数组元素值的一般格式： ${array_name[index]}
22. 获取数组中的所有元素
```
使用@ 或 * 可以获取数组中的所有元素，例如：
echo "数组的元素为: ${my_array[*]}"
echo "数组的元素为: ${my_array[@]}"
```
23. `获取数组的长度`
* 获取数组长度的方法与获取字符串长度的方法相同
```
echo "数组元素个数为: ${#my_array[*]}"
echo "数组元素个数为: ${#my_array[@]}"
```
```
A=1
my_array=($A B C D)
echo "第一个元素为: ${my_array[0]}"
```
24. `符号``为命令结果的表达`
* 小数计算，也需要配合bc计算器使用，个人感觉跟echo一样
* 没有``的时候
```
galen@galen-virtual:~$ cat add.sh 
#!/bin/sh
i=1.2
j=2.2
c=expr "$i + $j" | bc
echo $c
```
```
./add.sh: 4: ./add.sh: 1.2 + 2.2: not found

galen@galen-virtual:~$ 
```
* 有``的时候
```
galen@galen-virtual:~$ cat add.sh 
#!/bin/sh
i=1.2
j=2.2
c=`expr "$i + $j" | bc`
echo $c
```
```
galen@galen-virtual:~$ ./add.sh 
3.4
```
25. `两点注意`
```
表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2，这与我们熟悉的大多数编程语言不一样。
完整的表达式要被 ` ` 包含，注意这个字符不是常用的单引号，在 Esc 键下边。
```
26. `条件表达式`
* 注意：条件表达式要放在方括号之间，并且要有空格，例如: [$a==$b] 是错误的，必须写成 [ $a == $b ]
27. `条件表达式实例`
```
a=10
b=20

val=`expr $a + $b`
echo "a + b : $val"

val=`expr $a - $b`
echo "a - b : $val"

val=`expr $a \* $b`
echo "a * b : $val"

val=`expr $b / $a`
echo "b / a : $val"

val=`expr $b % $a`
echo "b % a : $val"

if [ $a == $b ]
then
   echo "a 等于 b"
fi
if [ $a != $b ]
then
   echo "a 不等于 b"
fi
```
28. 
```
* 乘号(*)前边必须加反斜杠(\)才能实现乘法运算；
* if...then...fi 是条件语句，后续将会讲解。
```
29. `运算符略写符`
```
EQ 就是 EQUAL等于
NQ 就是 NOT EQUAL不等于 
GT 就是 GREATER THAN大于　 
LT 就是 LESS THAN小于 
GE 就是 GREATER THAN OR EQUAL 大于等于 
LE 就是 LESS THAN OR EQUAL 小于等于
```
30. `read 命令从标准输入中读取一行,并把输入行的每个字段的值指定给 shell 变量`
```
#!/bin/sh
read name 
echo "$name It is a test"
以上代码保存为 test.sh，name 接收标准输入的变量，结果将是:
[root@www ~]# sh test.sh
OK                     #标准输入
OK It is a test        #输出
```
31. `显示`
```
* echo -e "OK! \n" # -e 开启转义 \n 换行
* echo -e "OK! \c" # -e 开启转义 \c 不换行
```
32.`echo '$name\"'` 
```
* 原样输出字符串，不进行转义或取变量(用单引号)
```
33. `显示执行时间`
```
* 显示命令执行结果
```
34. `echo输出的字符串总结`
```
===================================================================
       能否引用变量  |  能否引用转移符  |  能否引用文本格式符(如：换行符、制表符)
单引号  |           否           |             否             |                             否
双引号  |           能           |             能             |                             能
无引号  |           能           |             能             |                             否                          
===================================================================
```