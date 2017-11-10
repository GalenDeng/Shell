## echo和printf (2017.11.10)
* Shell 的输出命令 printf echo
```
printf 命令模仿 C 程序库（library）里的 printf() 程序。
标准所定义，因此使用printf的脚本比使用echo移植性好。
printf 使用引用文本或空格分隔的参数，外面可以在printf中使用格式化字符串，还可以制定字符串的宽度、左右对齐方式等。默认printf不会像 echo 自动添加换行符，我们可以手动添加 \n
```
```
$ echo "Hello, Shell"
Hello, Shell
$ printf "Hello, Shell\n"
Hello, Shell
```
1. `格式替代符`
```
%s %c %d %f都是格式替代符
%-10s 指一个宽度为10个字符（-表示左对齐，没有则表示右对齐），任何字符都会被显示在10个字符宽的字符内，如果不足则自动以空格填充，超过也会将内容全部显示出来。
%-4.2f 指格式化为小数，其中.2指保留2位小数
```
2. `默认值`
```
# 如果没有 arguments，那么 %s 用NULL代替，%d 用 0 代替
printf "%s and %d \n" 
```
3. `转义字符表`
*  ![转义字符表](https://github.com/GalenDeng/Shell/blob/master/printf%E7%9A%84%E8%BD%AC%E4%B9%89%E5%AD%97%E7%AC%A6.png)

4. `格式替代符详解`
```
%d %s %c %f 格式替代符详解:
d: Decimal 十进制整数 -- 对应位置参数必须是十进制整数，否则报错！
s: String 字符串 -- 对应位置参数必须是字符串或者字符型，否则报错！
c: Char 字符 -- 对应位置参数必须是字符串或者字符型，否则报错！
f: Float 浮点 -- 对应位置参数必须是数字型，否则报错！
如：其中最后一个参数是 "def"，%c 自动截取字符串的第一个字符作为结果输出。
$  printf "%d %s %c\n" 1 "abc" "def"
1 abc d
```