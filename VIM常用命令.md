1、:w[file]  另存为file

2、:r[file]  将[file]的内容加到光标行后面

3、:[m]，[n]w[file]  将m到n的内容保存为[file]

4、:s/old/new  替换当前行中第一个old为new

:s/old/new/g  替换当前行中所有old为new

:[m]，[n]s/old/new  替换m到n行中第一个old为new

:[m]，[n]s/old/new/g  替换m到n行中所有old为new

:%s/old/new/g  替换全文中所有old为new

例子：:20,40s/\/*  将20到40行的\替换为*

5、[n]dd  删除本行向下n行

[n]yy  复制本行向下n行

[n]x  删除n个字符

p  粘贴复制文本

u  撤销前一步操作

6、[n]↓  向下移动n行

[n]→  向右移动n行

gg  移动到第一行

G  移动到最后一行

[n]G  移动到第n行

7、yG  复制至文件尾

ggyG  复制文件头至文件尾

y$  复制光标处至行尾

y^  复制光标处至行首

8、/word  向下查找word字符串

？**word**  向上查找word字符串

9、:Tlist  打开函数列表  crtl+ww 窗口间切换，关闭同样用：Tlist

10、多行编辑  crtl+v，上下移动光标用来选中多行  Shift+I 编辑插入内容，Esc，Esc

多行缩进**  **crtl+v，上下移动光标用来选中多行  ，“<” (或者 “>”)用来减少缩进（增加缩进），“=”用来自动缩进

11、VIM调用shell命令

:！command  不退出vim，执行命令后结果在命令区域，不会改变文件内容

:r!command  不退出vim，执行命令后结果插入到当前行的下一行

:[m]，[n]w!command  将m到n行的内容输入到shell命令由command中处理，执行命令后结果在命令区域，不会改变文件内容

:[m]，[n]!command  将m到n行的内容输入到shell命令由command中处理，执行命令后结果替换m到n指定范围内内容

例子：:62!tr a-z  将62行的小写字母转为大写字母

12、打开多个文本**  :**vsp 左右分屏 :sp 左右分屏 crtl+ww窗口切换 :q  退出

例子：:vsp CameraTestBase.h

vim file1 同时打开file1和file2

:n  到前一个文件

:N  到后一个文件

:f  显示正在编辑文件的信息

 

 

 

 

 

 

 

 

 

Linux查找命令

表1 bash环境中的通配符

  符号****	意义****                                  
  *     	代表0个到无穷多个任意字符                           
  ？     	代表一定有一个任意字符                             
  []    	同样代表一定有一个在中括号内的字符（非任意字符）。  例如：[abcd]代表一定有一个字符，可能是a,b,c,d中的任一个
  [-]   	若有减号在中括号内时，代表在编码顺序内的所有字符。  例如：[0-9]代表0到9之间的所有数字。
  [^]   	若中括号内的第一个字符为指数符号（^），那代表反向选择。  例如：abc代表一定有一个字符，只要是非a,b,c的其他字符就接受。

 

1.grep命令和正则表达式的简介

(1)、grep(Global search REgular expression andPrint out the line)，即全局搜索正则表达式并打印出匹配的行，它是Linux系统中一个强大的文本搜索工具，它根据用户指定的“模式(pattern)”对目标文本进行过滤，显示被模式匹配到的行；

(2)、正则表达式是由一类字符书写的模式，其中有些字符不表示符的字面意义，而是表示控制或通配的功能

2.grep命令的基本语法格式

grep OPTION... 'PATTERN' FILE...

grep的[OPTION]：

    -v : 对匹配的行进行取反

    -o : 仅显示匹配到的内容

    -i : 忽略字符大小写

-n : 为匹配的行加上行号

-r:递归查找子目录

    -E : 使用扩展正则表达式 ,等同于egrep命令

    -F : 不使用正则表达式搜索，等同于fgrep命令

    -A # : 连同匹配行的下#行一并显示，#代表任意数字

    -B # : 连同匹配行的上#行一并显示，#代表任意数字

    -C # : 连同匹配行的上下#行一并显示，#代表任意数字

    --color=auto : 对匹配的内容以不同的颜色显示

3.grep正则表达式的基本用法

基本正则表达式：

(1)字符匹配

. : 匹配任意单个字符

    例：匹配以r开头，t结尾中间只隔了两个字符的行

    

[] : 匹配指定集合中的任意单个字符

常用的集合表示方法有：

        纯数字：[[:digit:]]或[0-9]

        小写字母：[[:lower:]]或[a-z]

        大写字母：[[:upper:]]或[A-Z]

        大小写字母：[[:alpha:]]或[a-zA-Z]

        数字加字母：[[:alnum:]]或[0-9a-zA-Z]

        空白字符：[[:space:]]

        标点符号：[[:punct:]]

    例1：匹配包含数字0或2的行(截图只包含前半部分)

    

    例2：匹配包含字母r或t的行(截图只包含前半部分)

    

    例3：匹配包含数字0-9的行(截图只包含前半部分)

    

[^] : 匹配指定集合外的任意单个字符

    例：匹配包含除1-9范围之外的字符的行(截图只包含前半部分)

    

(2)次数匹配

* : 匹配其前面的字符出现任意次，0、1或多次的行

    例：创建一个测试文本，包含有以下内容：

    

    匹配x字母出现任意次的行：

    

+ : 匹配其前面的字符出现1次或多次的行

    例：匹配x字至少1次的行

    

\? : 匹配其前面的字符出现0次或1次的行

    例：匹配x字母出现0次或1次的行

    

{m} : 匹配其前面的字符出现m次的行

    例：匹配x字母出现2次的行

    

{m,n} : 匹配其前面的字符至少出现m次，至多出现n次的行，m和n表示一个范围m-n

    例：匹配x字母至少出现1次，至多出现3次的行

    

(3)位置锚定

^ : 行首锚定

    例：匹配x字母出现在在行首的行

    

$ : 行尾锚定

    例：匹配e字母出现在行尾的行

    

^$ : 匹配空白行

    例：匹配空白的行

    

< : 词首锚定

    例：精确匹配xy两个字母在一个单词的词首的行

    

> : 词尾锚定

    例：精确匹配xy两个字母在一个单词的词尾的行

    

<> : 匹配单词

    例：匹配包含xy这个单词的行

    

(3)分组

 (): 对某字符串进行进行分组匹配

    例：匹配xy单启出现0次或1次的行

    

后向引用：模式中，如果使用  ()实现了分组，在某行文本的检查中，如果  ()的模式匹配到了某内容，此内容后面的模式中可以被引用；

对前面的分组进行引用的符号为：\1 , \2 ,\3

模式自左而右，引用第#个左括号以及与其匹配右括号之间的模式匹配到的内容；

后向引用举例：

    新建一个文本文件，假设有如下内容：

    

    找出前后都有相同单词的行：

    

正则表达式元字符总结：

    字符匹配：. ，[] ，[^]

    次数匹配：* ，\? ，+ ，{m}，{m,n}

    位置锚定：^ ，$ ，< ，>，<>

    分组匹配：  ()

4.egrep及扩展正则表达式：

egrep相当于grep -E，egrep可以直接使用扩展正则表达式，而grep需要加上选项-E；

扩展正则表达式的元字符：

    字符匹配：. ，[] ，[^]

    次数匹配：*，?，+，{m}，{m,n}，{m,}，{0,n}

    位置锚定：^，$，>，<

    分组匹配：()，支持后向引用

    | ： 匹配左侧或右侧符合条件的行，比如a|b，含有a或b的行都匹配；

    例1：egrep 等同于 grep -E

    

    例2：

    

5.grep练习题：

(1).显示/proc/meminfo文件中以大写或小写s开头的行；

# grep -i '^s' /proc/meminfo

(2).显示/etc/passwd文件中其默认shell为非/sbin/nologin的用户；

# grep -v '/sbin/nologin$' /etc/passwd | cut -d: -f1

(3).显示/etc/passwd文件中其默认shell为/bin/bash的用户

进一步：仅显示上述结果中其ID号最大的用户

# grep '/bin/bash$' /etc/passwd | cut -d: -f1 | sort -n -r | head -1

(4).找出/etc/passwd文件中的一位数或两位数；

# grep '<[[:digit:]]{1,2}>' /etc/passwd

(5).显示/boot/grub/grub.conf中至少一个空白字符开头的行

# grep '^[[:space:]]+.*' /boot/grub/grub.conf

(6).显示/etc/rc.d/rc.sysinit文件中，以#开头，后面跟至少一个空白字符，而后又有至少一个非空白字符的行；

# grep '^#[[:space:]]+[:space:]+' /etc/rc.d/rc.sysinit

(7).找出netstat -tan命令执行结果中包含'LISTEN'的行；

# netstat -tan | grep 'LISTEN[[:space:]]*$

(8).添加用户bash,testbash,basher,nologin(SHELL为/sbin/nologin)，而找出当前系统上其用户名和默认SHELL相同的用户；

# grep '<[[:alnum:]]+  ().*\1$'/etc/passwd

(9).扩展题：新建一个文本文件，假设有如下内容：

He like his lover.

He love his lover.

He like his liker.

He love his liker.

找出其中最后一个单词是由此前某单词加r构成的行；

# grep '<[[:alpha:]]+  ().*\1r'grep.txt

(10).显示当前系统上root、centos或user1用户的默认shell及用户名；

# grep -E '^(root|centos|user1>)' /etc/passwd

(11).找出/etc/rc.d/init.d/functions文件中某单词后面跟一对小括号'()"的行；

# grep -o '<[[:alpha:]]+>()' /etc/rc.d/init.d/functions

(12).使用echo输出一个路径，而使用egrep取出其基名；

# echo/etc/rc.d/ | grep -o '/+/\?$' | grep -o '/+'
