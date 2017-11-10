## shell流程控制 (2017.11.10)
1. `和Java、PHP等语言不一样，sh的流程控制不可为空，如(以下为PHP流程控制写法)：` 
```
<?php
if (isset($_GET["q"])) {
    search(q);
}
else {
    // 不做任何事情
}
```
* 在sh/bash里可不能这么写，如果else分支没有语句执行，就不要写这个else
2. `if else-if else`
```
if condition1
then
    command1
elif condition2 
then 
    command2
else
    commandN
fi
```
3. `if与test连用`
```
if else语句经常与test命令结合使用，如下所示：
num1=$[2*3]
num2=$[1+5]
if test $[num1] -eq $[num2]
then
    echo '两个数字相等!'
else
    echo '两个数字不相等!'
fi
```
4. `for语句`
* `in列表是可选的`，如果不用它，for循环使用命令行的位置参数
```
for loop in 1 2 3 4 5
do
    echo "The value is: $loop"
done
输出结果：
The value is: 1
The value is: 2
The value is: 3
The value is: 4
The value is: 5
```
```
for str in 'This is a string'
do
    echo $str
done
输出结果：
This is a string
```
5. `while语句`
* 使用了` Bash let 命令`，它`用于执行一个或多个表达式`，变量计算中`不需要加上 $ 来表示变量`
```
#!/bin/sh
int=1
while(( $int<=5 ))
do
    echo $int
    let "int++"
done
运行脚本，输出：
1
2
3
4
5
```
* while循环`可用于读取键盘信息`。下面的例子中，输入信息被设置为变量FILM，按<Ctrl-D>结束循环
```
echo '按下 <CTRL-D> 退出'
echo -n '输入你最喜欢的网站名: '
while read FILM
do
    echo "是的！$FILM 是一个好网站"
done
运行脚本，输出类似下面：
按下 <CTRL-D> 退出
输入你最喜欢的网站名:菜鸟教程
是的！菜鸟教程 是一个好网站
```
* `无限循环`
1. 
```
while :
do
    command
done
```
2. 
```
while true
do
    command
done
```
3. 
```
for (( ; ; ))
```
6. `case语句`
```
echo '输入 1 到 4 之间的数字:'
echo '你输入的数字为:'
read aNum
case $aNum in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3)  echo '你选择了 3'
    ;;
    4)  echo '你选择了 4'
    ;;
    *)  echo '你没有输入 1 到 4 之间的数字'
    ;;
esac
```
7. `break命令`
```
#!/bin/bash
while :
do
    echo -n "输入 1 到 5 之间的数字:"
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的! 游戏结束"
            break
        ;;
    esac
done
```
8. `continue`
```
#!/bin/bash
while :
do
    echo -n "输入 1 到 5 之间的数字: "
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的!"
            continue
            echo "游戏结束"
        ;;
    esac
done
```
* 运行代码发现，当输入大于5的数字时，该例中的循环不会结束，语句 echo "Game is over!" 永远不会被执行