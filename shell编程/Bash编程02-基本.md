# 3. 特殊字符
- \#  
注释。行首以#（#!是一个例外）开头是注释。注释也可以放在与本行命令的后边。注释也可以放在本行行首空白的后面。  
命令是不能放在同一行注释的后边的。应为没有办法把注释结束掉，好让同一行后边的‘代码生效’。只能够另起一行来使用下一个命令。  
在echo中转义的#是不能作为注释的，同样地，#也可以出现在特定的参数替换结构中，或者出现在数字常量表达式中。
标准的引用和转义字符'\'可以用来转义#。
某些特定的模式匹配操作也可以使用#。  

- ；
命令分隔符[分号,即;].可以在同一行上写两个或两个以上的命令。
注意：';'某些情况下需要转义

- ;;
终止case选项[双分号，即;;]。

- .
‘点’命令[句点，即'.']。等价于source命令，这是一个bash的内建命令。

- .
  '点'作为文件名的一部分。如果点放在文件名的开头的话，那么这个文件将会成为隐藏文件，并且ls命令将不会正常显示出这个文件。
如果作为目录名的话，一个单独的点代表当前的工作目录，而两个点表示上一级目录。点经常出现在文件移动命令的目的参数（目录）的位置上。

- .
'点'字符匹配。当用作匹配字符的作用时，通常都是作为正则表达式的一部分来使用，’点’用来匹配任何的单个字符。

- "
部分引用[双引号,即 "]，"STRING"将会阻止（解释）STRING大部分特殊的字符。

- '
全引用[单引号，即']，'string'将会阻止string中所有的特殊字符的解释。这是一种比使用"更强烈的形式。

- ,
逗号操作符。逗号操作符链接了一系列的算数操作，虽然里面所有的内容都被运行了，但只有最后一项被返回。
  ​    let "t2 = ((a = 9, 15 / 3))" # Set "a = 9" and "t2 = 15 / 3"    
- \
转义符[反斜线，即\\],一种对单字符的引用机制。\\X将会"转义"字符X. 这等价于"X", 也等价于'X'. \\通常用来转义"和', 这样双引号和但引号就不会被解释成特殊含义了.

- /
文件名称路径分隔符[斜线，即/]。分割文件名不同的部分，也可以用来作为除法的算术操作符。

- \`
命令替换。\`command\`结构可以将命令的输出赋值到一个变量中去。

- :
空命令[冒号，即:]。等价于“NOP”（no op，一个什么都不干的命令）。也可以被认为与shell内建命令true作用相同，”:”命令是个bash的内建命令，它的退出码时true。
死循环 while :
if/then中的占位符：
  ​    if condition
  ​    then : # 什么都不做，引出分支。
  ​    else
  ​      todo
  ​    fi
在一个二元命令中提供一个占位符。  
在here document中提供一个命令所需的占位符。
使用参数替换来评估字符串变量。  
变量扩展/子串替换。  
在与 > 重定向操作符结合使用，将会把一个文件情况，但是并不会修改这个文件的权限。如果这个文件不存在，那么创建这个文件。
在与 >> 重定向操作符结合使用时，将不会对预先存在的目标文件(: >> target-file)产生任何影响。如果文件不存在，则创建。  
也可以用来作为注释行，虽然不推荐那么做。
‘:’还用来在/etc/passwd和$PATH变量中做分隔符。  

- !
取反操作符[叹号,即!]. !操作符将会反转命令的退出码的结果。也会反转测试操作符的意义，! 操作符时Bash的关键字。  
在一个不同的上下文中，!也会出现在变量的间接引用中。

- \*
通配符[星号，即*].\*可以用来做文件名匹配的通配符，含义是，可以用来匹配给定目录下的任何文件名。  
\*用在正则表达式中，用来匹配任意个数的字符。

- \*
算术操作符。在算术操作符的上下文中，\*表示乘法运算，如果要做幂运算，使用**,这是求幂操作符

- ?
测试操作符。在一个特定的表达式中，?用来测试一个条件的结果。  
在一个双括号的结构中，?就是C语言的三元操作符  
在参数替换表达式中，?用来测试一个变量是否被set.

- ?
通配符。?在通配中，用来匹配单个字符的“通配符”，在正则表达式中，也是用来表示一个字符.

- $
变量替换（引用变量的内容）

- $
行结束符，在正则表达式中，”$”表示行结束符。

- ${}
  参数替换

- $* $@
位置参数

- $?
退出状态码变量，$?变量保存了一个命令，一个函数，或者时脚本本身的退出状态码

- $$
进程ID变量，这个$$变量包处理他所在的脚本的进程ID

- ()
命令组

    (a=hello; echo $a)

在括号中的命令列表，将会作为一个子shell来运行。父进程，脚本本身，不能读取在子进程中创建的变量。

初始化数组

    Array=(element1 element2 element3)

大括号扩展

    cat {file1,file2,file3} > combined_file
    # 把file1, file2, file3连接在一起, 并且重定向到combined_file中.


    cp file22.{txt,backup}
    # 拷贝"file22.txt"到"file22.backup"中
一个命令可能会对大括号中的以逗号分割文件的列表起作用，将对大括号中的文件名做扩展。

在大括号中，不允许有空白，除非这个空白被引用或转义。

- {}
代码块[大括号，即{}]又被称为内部组，这个结构事实上创建了一个匿名函数。与标准函数不同的是，在其中声明的变量，对脚本的其他部分的代码来说还是可见的。

例子3-1 代码块和I/O重定向

    #! /bin/bash
    # 从/etc/fstab中读行
    
    File=/etc/fstab
    {
      read line1
      read line2
    } < $File
    
    echo "First line in $File is: "
    echo "$line1"
    echo
    echo "Second line in $File is: "
    echo "$line2"
    
    exit 0
    # 现在，这么分析每行的分割域
    # 小提示，使用awk

例子3-2 将一个代码块的结果保存到文件
​    #! /bin/bash
​    # rpm-check.sh
​    # 这个脚本的目的是为了描述, 列表, 和确定是否可以安装一个rpm包.
​    # 在一个文件中保存输出.
​    #
​    # 这个脚本使用一个代码块来展示.
​    SUCCESS=0
​    E_NOARGS=65

    if [ -z "$1" ]
    then
      echo "Usage: `basename $0` rpm-file"
      exit $E_NOARGS
    fi
    
    {
      echo
      echo "Archive Description: "
      rpm -qpi $1  # 查询说明
      echo
      echo "Archive Listing: "
      rpm -qpl $1  # 查询列表
      echo
      rpm -i --test $1  # 查询rpm包是否可以被安装。
    
      if [ "$?" -eq $SUCCESS ]
      then
        echo "$1 can be installed."
      else
        echo "$1 cannot be installed."
      fi
      echo
    } > "$1.test" # 把代码块中的所有输出重定向到文件中。
    echo "resultes of rpm test in file $1.test"
    
    # 查看rpm的man页来查看rpm的选项。
    
    exit 0

- {} \;
 路径名，一般在find命令中使用，不是shell内建命令。

- [  ]
条件测试，条件测试表达式放在[  ]中。值得注意的是[ 是shell内建test命令的一部分，并不是/usr/bin/test中的外部命令的一个链接。  

- [[  ]]
测试。测试表达式放在[[]]中（shell关键字）

- [ ]
数组元素，在一个array结构的上下文中，中括号用来引用数组中每个元素的编号

- [ ]
字符范围，用做正则表达式的一部分，方括号描述一个匹配的字符范围

- (( ))
整数扩展，扩展并计算在(())中的整数表达式。

- \> &> >> < <>
> 重定向
scriptname >filename 重定向scriptname的输出到文件filename中. 如果filename存在的话, 那么将会被覆盖.
command &>filename 重定向command的stdout和stderr到filename中.
command >&2 重定向command的stdout到stderr中.
scriptname >>filename 把scriptname的输出追加到文件filename中. 如果filename不存在的话,将会被创建.
[i]<>filename 打开文件filename用来读写, 并且分配文件描述符i给这个文件. 如果filename不存在, 这个文件将会被创建.  
进程替换.
(command)>
<(command)
在一种不同的上下文中, "<"和">"可用来做 字符串比较操作.
在另一种上下文中, "<"和">"可用来做 整数比较操作.

- <<
> 用在here document中的重定向

- <<<
> 用在here string中的重定向

- <, >
> ASCII comparison

- \<, \>
> 正则表达式中的单词边界。

- |
> 管道，分析前边命令的输出，并将输出作为后边命令的输入，这是一种产生命令链的好方法。
管道是进程间通讯的一个典型办法，将一个进程的stdout放到另一个进程stdin中。标准的方法一般是将一个一般命令的输出，比如cat或者echo，传递到一个“过滤命令”中，然后得到结果。
当然输出命令也可传递到脚本中。

    #! /bin/bash
    # uppercash.sh : 修改输入，全部转换为大写
    tr 'a-z' 'A-Z'
    # 字符范围必须被''""引用起来
    #+ 阻止产生单字符的文件名.
    
    exit 0 

> 管道中的每个进程的stdout必须被下一个进程作为stdin来读入。否则，数据流会阻塞，并且管道将参生一些非预期的行为。
作为子进程的运行的管道，不能修改脚本的变量。
如果管道中的某一个命令产生了异常，并中途失败，那么这个管道将过早的终止。这种行为被叫做broke pipe，并且这种情况下将发送一个SIGPIPE信号。

- \>|
> 强制重定向，这将强制覆盖一个现存文件。

- || 
> 或-逻辑操作，在一个条件测试结构中，如果条件测试结构两边中任意一边结果为true的话，||操作就会返回0（代表操作成功）。

- &
> 后台运行命令。一个命令后边跟一个& 表示后台运行。
在一个脚本中，命令和循环都可能运行在后台
例子3-3 在后台运行一个循环

    #! /bin/bash
    # backgroud-loop.sh
    
    for i in 1 2 3 4 5 6 7 8 9 10 # 第一个循环
    do 
      echo -n "$i"
    done &  # 在后台运行这个循环
            # 在第2个循环之后，将在某些时候执行。
    
    echo    # 这个echo某些时候将不会显示
    
    for i in 11 12 13 14 15 16 17 18 19 20  #第二个循环
    do
      echo "$i"
    done
    echo    # 这个echo某些时候将不会显示
    # ======================================================
    
    # 期望的输出应该是:
    # 1 2 3 4 5 6 7 8 9 10
    # 11 12 13 14 15 16 17 18 19 20
    
    # 然而实际的结果有可能是:
    # 11 12 13 14 15 16 17 18 19 20
    # 1 2 3 4 5 6 7 8 9 10 bozo $
    # (第2个'echo'没执行, 为什么?)
    
    # 也可能是:
    # 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
    # (第1个'echo'没执行, 为什么?)
    
    # 非常少见的执行结果, 也有可能是:
    # 11 12 13 1 2 3 4 5 6 7 8 9 10 14 15 16 17 18 19 20
    # 前台的循环先于后台的执行.
    
    exit 0
    
    # Nasimuddin Ansari 建议加一句 sleep 1
    #+ 在6行和14行的 echo -n "$i" 之后加这句.
    #+

> 在一个脚本内后台运行一个命令，有可能造成这个脚本的挂起，等待一个按键相应。

- && 
> 与-逻辑操作。在一个条件测试结构中，只要条件测试两边结果都为true的时候，&&操作才会返回0（代表成功）

- \-
> 选项前缀.在所有的命令内如果想要使用选项参数的话，前边都要加上‘-’。

- \- 
> 用于重定向stdin或stdout[破折号，即-]
在需要一个文件名的位置，-重定向输出到stdout，或者stdin接受输入，而不是从一个文件中输入。这是在管道中使用文件导向（file-oriented）工具来作为过滤器的一种方法。
在命令行上单独给出一个file，会给出一个错误信息。添加一个‘-’将得到一个更有用的结果。这会使shell等待用户输入。
‘-’可以被用来将stdout通过管道传递到其他命令中。这样就运行使用在一个文件开头添加几行的技巧。
例子3-4 备份最后一天所以修改的文件

    #！ /bin/bash
    #  在一个"tarball"中(经过tar和gzip处理过的文件)
    #+ 备份最后24小时当前目录下d所有修改的文件.
    
    BACKUPFILE=backup-$(date +%m-%d-%Y)
    # 在备份文件中嵌入时间
    archive=${1:-$BACKUPFILE}
    #  如果在命令行中没有指定备份文件的文件名,
    #+ 那么将默认使用"backup-MM-DD-YYYY.tar.gz".
    tar cvf - `find . -mtime -l -type f -print` > $archive.tar
    gzip $archive.tar
    echo "Directory $PWD backed up in archvie file \"$archive.tar.gz\""
    #  Stephane Chazelas指出上边代码,
    #+ 如果在发现太多的文件的时候, 或者是如果文件
    #+ 名包括空格的时候, 将执行失败.
    
    # Stephane Chazelas建议使用下边的两种代码之一:
    # -------------------------------------------------------------------
    #   find . -mtime -1 -type f -print0 | xargs -0 tar rvf "$archive.tar"
    #      使用gnu版本的"find".


    #   find . -mtime -1 -type f -exec tar rvf "$archive.tar" '{}' \;
    #         对于其他风格的UNIX便于移植, 但是比较慢.
    # -------------------------------------------------------------------


    exit 0

> 以‘-’开头的文件名在使用‘-’作为重定向操作符的时候，可能会产生问题。应该写一个脚本来检查这个文本，并给这个文件加上合适的前缀。
如果变量以 - 开头命名，可能也会引起问题。

- \- 
>先前的工作目录。cd - 将会回到先前的工作目录。使用了$OLDPWD环境变量。对于‘-’的具体解释只能依赖于具体的上下文。

- \-
>减号。减号属于算术操作

- =
>等号。赋值操作
在另一种上下文环境中，=也用来做字符串比较操作。

- \+
> 加号。加法算术操作。
在另一种上下文环境中，+也是一种正则表达式操作

- \+
> 选项.一个命令或者过滤器的选项标记
某些命令内建命令使用+来打开特定的选项,用-来禁用这些特定的选项

- % 
> 取模. 取模算术操作.
在不同上下中,%也是一种模式匹配操作

- ~
> home目录[波浪号,~].相当于$HOME内部变量.

- ~+
> 当前工作目录,相当于$PWD变量

- ~-
> 先前的工作目录.相当于$OLDPWD内部变量.

- =~
> 正则表达式匹配

- ^
行首.在正则表达中,"^"表示定位到文本行的行首.

# 控制字符

> 修改终端或文本显示的行为. 控制字符以CONTROL+key这种方式进行组合(同时按下).控制字符也可以使用8进制或16进制表示法来进行表示,但是前边必须要加上转义符.
控制脚本在脚本中不能正常使用.

- Ctl-B
> 退格(非破坏性的), 就是退格但是不删掉前面的字符.
- Ctl-C
> break. 终结一个前台作业.

- Ctl-D
> 从一个shell中登出(与exit很相像).
"EOF"(文件结束). 这也能从stdin中终止输入.
在console或者在xterm窗口中输入的时候, Ctl-D将删除光标下字符. 当没有字符时, Ctl-
D将退出当前会话, 在一个xterm窗口中, 则会产生关闭此窗口的效果.

- Ctl-G
> "哔" (beep

- Ctl-H
> "退格"(破坏性的), 就是在退格之后, 还要删掉前边的字符.

- Ctl-I
> 水平制表符.

- Ctl-J
> 重起一行(换一行并到行首). 在脚本中, 也可以使用8进制表示法 -- '\012' 或者16进制
表示法 -- '\x0a' 来表示.

- Ctl-K
> 垂直制表符.
当在console或者xterm窗口中输入文本时, Ctl-K将会删除从光标所在处到行为的全部字
符. 在脚本中, Ctl-K的行为有些不同, 具体请参见下边的Lee Maschmeyer的例子程序.

- Ctl-L
>清屏(清除终端的屏幕显示). 在终端中, 与clear命令的效果相同. 当发送到打印机上时,
Ctl-L会让打印机将打印纸卷到最后.

- Ctl-M
>回车.

- Ctl-Q
> 恢复(XON).
在一个终端中恢复stdin.

- Ctl-S
>挂起(XOFF).
在一个终端中冻结stdin. (使用Ctl-Q可以恢复输入.)

- Ctl-U
> 删除光标到行首的所有字符. 在某些设置下, 不管光标的所在位置Ctl-U都将删除整行输
入.

- Ctl-V
>当输入字符时, Ctl-V允许插入控制字符. 比如, 下边的两个例子是等价的:
  1 echo -e '\x0a'
  2 echo <Ctl-V><Ctl-J>
Ctl-V主要用于文本编辑.

- Ctl-W
> 当在控制台或一个xterm窗口敲入文本时, Ctl-W将会删除当前光标到左边最近一个空格间
的全部字符. 在某些设置下, Ctl-W将会删除当前光标到左边第一个非字母或数字之间的全
部字符.

- Ctl-Z
> 暂停前台作业.

- 空白
> 用来分隔函数,命令或变量.空白包含空格,tab,空行或者他们之间的任意的组合体.
空行不会影响脚本的行为,特殊变量$IFS用来做一些输入命令的分隔符,默认情况下是空白.
如果想在字符串或变量中使用空白,那么应该使用引用.

# 4. 变量和参数的介绍

> 变量是脚本编程中进行数据表现的一种方法.
变量既可以出现在算术操作中,也可以出现在字符串分析过程中.

## 4.1 变量替换

> 变量的名字就是变量保存值的地方.引用变量的值就叫做变量替换.

- $
> 如果var是一个变量的名字,那么\$var就是引用这个变量的值,即变量所包含的数据.
当变量"裸体"出现的时候 -- 也就是说没有\$前缀的时候 -- 那么变量可能存在如下几种情况.变量被声明或被赋值, 变量被unset, 变量被exporte, 或者是变量处在一种特殊的情况 -- 变量代表一种信号.
被一对双引号(" ")括起来的变量替换是不会被阻止的. 所以双引号被称为部分引用, 有时候又被称为"弱引用". 但是如果使用单引号的话(' '), 那么变量替换就会被禁止了, 变量名只会被解释成字面的意思, 不会发生变量替换. 所以单引号被称为全引用, 有时候也被称为"强引用".
注意\$variable事实上只是\${variable}的简写形式. 在某些上下文中\$variable可能会引起错误,这时候你就需要用\${variable}了

例子 4-1 变量赋值和替换

    #! /bin/bash
    # 变量赋值和替换
    a=375
    hello=$a
    # 强烈注意, 在赋值的的时候, 等号前后一定不要有空格.
    echo hello
    echo $hello
    echo ${hello}
    
    echo "$hello"
    echo "${hello}"
    
    echo 
    
    hello="A B C   D"
    echo $hello
    echo "$hello"
    
    echo '$hello'
    # 全引用的作用将会导致"$"被解释为单独的字符,而不是变量前缀.
    
    hello=  # 设置为空值.
    echo "\$hello (null value) = $hello"
    
    # 可以在同一行上设置多个变量,但是必须以空白进行分隔,慎用,降低可读性,并且不可移植.
    var1=21 var2=22 var3=$V3
    echo
    echo "var1=$var1 var2=$var2 var3=$var3"
    
    echo; echo
    numbers="one two three"
    other_numbers="1 2 3"
    # 如果变量中存在空白,那么就必须加上引用.
    echo "numbers = $numbers"
    echo "other_numbers = $other_numbers"
    
    echo "$mixed_bag"
    echo; echo
    echo "uninitialized_variable = $uninitialized_variable"
    # Uninitialized变量为null(就是没有值). 
    uninitialized_variable=   #  声明, 但是没有初始化这个变量, 
                              #+ 其实和前边设置为空值的作用是一样的. 
    echo "uninitialized_variable = $uninitialized_variable"
                              # 还是一个空值.
    
    uninitialized_variable=23       # 赋值.
    unset uninitialized_variable    # Unset这个变量.
    echo "uninitialized_variable = $uninitialized_variable"
                                    # 还是一个空值.
    echo
    
    exit 0

> 一个未初始化的变量将会是null值,就是未赋值(但不是代表值0)    

## 4.2 变量赋值

- = 
> 赋值操作(前后都不能有空白)
注意: = 既可以用作条件测试操作,也可以用于赋值操作,这需要是具体的上下文而定

> 例子4-2 简单的变量赋值

    #! /bin/bash
    # '裸体变量'
    echo
    
    # 变量什么时候是"裸体"的,当它被赋值的时候,而不是被引用的时候
    # 赋值
    a=879
    echo "the value of \"a\" is $a."
    
    # 使用'let'赋值
    let a=16+5
    echo "the value of \"a\" is now $a."
    
    echo
    
    # 在for循环中(事实上,这是一种未赋值)
    echo -n "Values of \"a\" in the loop are: "
    for a in 7 8 9 11
    do 
    echo -n "$a "
    done
    
    echo
    echo 
    # 使用read命令进行赋值
    echo -n "enter \"a\""
    read a
    echo "The value of \"a\" is now $a."
    echo 
    exit 0

> 例子4-3 简单和复杂,两个类型的变量赋值

    #! /bin/bash
    a=23
    echo $a
    b=$a
    echo $b
    
    a=`echo Hello`  # 把'echo'命令的结果传给变量'a'
    echo $a
    
    a=`ls -l`
    echo $a # 如果没有引号的话将会删除ls结果中多余的tab和换行符.
    echo 
    echo "$a" # 如果加上引号的话, 那么就会保留ls结果中的空白符.
    
    exit 0

> 使用$(..)机制来进行变量赋值.

##　4.3 Bash变量是不区分类型的.
> 本质上,Bash变量都是字符串.但是依赖于具体的上下文,Bash也允许比较操作和整数操作.其中的关键因素就是,变量中的值是否只含有数字
例子4-4 整形还是字符串

    #! /bin/bash
    # init-or-string.sh : 整型还是字符串
    
    a=2334              # 整型
    let "a += 1"        
    echo "a = $a"       # a=2335 还是整型
    echo
    
    b=${a/23/BB}        # 将"23"替换为"BB" b为字符串
    echo "b = $b"               
    declarre = -i b     # 即使使用declare命令也不会改变b的类型
    echo "b = $b"
    
    let "b += 1"    
    echo "b = $b"
    echo
    
    c=BB34
    echo "c = $c"
    d=${c/BB/23}        # 这将使$d变为整型
    echo "d = $d"
    let "d += 1"
    echo "d = $d"
    echo
    
    # null变量
    e=""
    echo "e = $e"
    let "e += 1"
    echo "e = $e"   # null变量被转换成一个整型变量
    echo
    
    echo "f = $f"
    let "f += 1"
    echo "f = $f"   # 未声明的变量转换成一个整型变量
    echo 
    # 所以所bash中变量都是不区分类型的.
    exit

## 4.4 特殊的变量类型
- 局部变量
> 这种变量只有在代码块或者函数中才可见
- 环境变量
> 这种变量将影响用户接口和shell的行为
分配给环境变量的空间是有限的.创建太多的环境变量,或者给一个环境变量分配太多的空间都会引起错误.
- 位置参数
> 从命令行传递到脚本的参数:$0 $1 $2 $3 ...
$0 就是脚本文件自身的名字,$1第一个参数,$9之后就必须用大括号括起来了,比如,${10}
两个比较特殊的变量$*和$@表示所有的位置参数

例子4-5 位置参数

    #! /bin/bash
    # 作为用例,调用这个脚本只是需要10个参数
    MINPARAMS=10
    
    echo
    
    echo "The name of this script is \"$0\"."
    # 添加./是表示当前目录
    echo "The name of this script is \"`basename $0`\""
    # 去掉路径名,剩下文件名
    
    echo
    if [ -n "$1" ]
    then
        echo "parameter #1 is $1"
    fi
    
    if [ -n "$1" ]
    then
        echo "parameter #1 is $1"
    fi
        if [ -n "$2" ]
    then
        echo "parameter #2 is $2"
    fi
        if [ -n "$3" ]
    then
        echo "parameter #3 is $3"
    fi
        if [ -n "$4" ]
    then
        echo "parameter #4 is $4"
    fi
        if [ -n "$5" ]
    then
        echo "parameter #5 is $5"
    fi
        if [ -n "$6" ]
    then
        echo "parameter #6 is $6"
    fi
        if [ -n "$7" ]
    then
        echo "parameter #7 is $7"
    fi
    if [ -n "$8" ]
    then
        echo "parameter #8 is $8"
    fi
        if [ -n "$9" ]
    then
        echo "parameter #9 is $9"
    fi
        if [ -n "${10}" ]
    then
        echo "parameter #10 is ${10}"
    fi
    
    echo "--------------------------------------"
    echo "All the command-line parameters are: "$*""
    
    if [ $# -lt "$MINPARAMS" ]
    then
        echo
        echo "This script needs at least $MINPARAMS command-line arguments!"
     fi
     
     echo 
     
     exit 0

> {}标记法提供了一种提取从命令行传递到脚本的最后一个位置的参数的简单办法.但是这种方法还需要使用间接引用.

# 引用
> 引用的字面以所就是将字符串用双括号括起来.它的的作用就是保护字符串中的特殊字符不被shell或者shell脚本重新解释或者扩展.
## 5.1  引用变量
> 在一个双引号中通过直接使用变量名的方法来引用变量,一般情况下都是没问题的.但是$,`和\除外.

> 使用刷引号还能阻止单词分割.如果一个参数被双引号括起来的话,那么这个参数将认为是一个单元,即使这个参数包含空白,那里面的单词也不会被分开.
在echo语句中,只有在单词分割或者需要保留空白的时候,才需要把参数用双引号括起来.

例子 5-1 ehco出一些诡异的变量

    #! /bin/bash
    # weirdvars.sh echo 出一些诡异变量
    var="'([\\{}\$\""
    echo $var
    echo "$var"
    echo
    IFS='\'
    echo $var       # \ 字符被空白字符替换了
    echo "$var"
    
    exit 0

> 单引号(' ')操作与双引号基本一样,但是不允许引用变量.

## 5.2  转义
> 转义是一种引用单个字符的方法. 一个前面放上转义符(\)的字符就是告诉shell这个字符按照字面的意思进行解释,即这个字符失去了它的特殊含义.  
- 特定的转义符的特殊含义
> echo 和 sed 命令中使用

- \n    表示新的一行
- \r    表示回车
- \t    表示水平制表符
- \v    表示垂直制表符
- \b    表示后退符
- \a    表示alert
- \0xx  转换为八进制的ASCII码,等价于0xx

例子 5-2 转义符

    #! /bin/bash
    # excaped.sh: 转义符
    echo; echo
    echo "\v\v\v\v" # 逐字打印\v\v\v\v
    # 使用-e选项的'echo'命令来打印转义符
    echo "================================"
    echo "VERTICAL TABS"
    echo -e "\v\v\v\v"
    echo "================================"
    echo "QUOTATION MARK"
    echo -e "\042"
    echo "================================"
    
    # 如果使用$'\X'结构,那-e选项就不必要了
    echo; echo "NEWLINE AND BEEP"
    echo $'\n'
    echo $'\a'
    echo "================================"
    echo "QUOTATION MARKS "
    echo $'\t \042 \t'
    echo $'\t \x22 \t'
    echo "================================"
    echo
    
    # 分配ASCII字符到变量中
    quote=$'\042'
    echo "$quote This is a quoted string, $quote and this lies outside the quotes"
    echo
    
    # 变量中连续的ASCII字符
    triple_underline=$'\137\137\137'
    echo "$triple_underline" UNDERLINE $triple_underline"
    echo
    
    ABC=$'\101\102\103\010'
    echo $ABC
    echo;echo
    escape=$'\033'
    echo "\"escape\" echoes as $escape"
    
    echo; echo
    exit 0

- \\"    表示引号字面的意思
- \\$    表示$本身字面的含义
- \\\    表示反斜线字面的意思

# 6. 退出和退出状态码
> exit 被用来结束一个脚本.返回一个值,这个值会传递给脚本的父进程,父进程会使用这个值做下一步处理.  
每个命令都会返回一个退出状态码.成功的命令返回0,而不成功的命令返回非零值,非零值通常被解释成一个错误码.  
当脚本以不带参数的exit命令结束时.脚本的退出状态码就由脚本中最后执行的命令来决定.不带参数的exit命令与exit $?的效果是一样的.
甚至脚本结尾不写exit,也与前两者的效果相同.  
$? 保存最后所执行的命令的退出状态码.当函数返回之后,$?保存函数中最后所执行的命令的退出状态码.这就是bash对函数"返回值"的处理方法.
当一个脚本退出,$?保存了脚本的退出状态码.一般情况下0表示成功,在范围1-255的整数表示错误.

$? 用于测试脚本中的命令结果的时候,往往显得特别有用.
> !, 逻辑非操作符,将会反转命令或条件测试的结果,并且这会影响退出状态码.  
特定的退出状态码具有保留意思,所以用户不应该在脚本中指定它.

# 7. 条件判断

​	每个完整并且合理的程序语言都具有条件判断的功能,并且可以根据测试的结果做下一步的处理.Bash有test命令,各种中括号和圆括号操作和if/then结构.

## 7.1 条件测试结构

1. if/then结构用来判断命令列表的退出状态码是否为0, 如果成功的话,那么执行接下来的一个或者多个命令.

2. 有一个专有命令[ (左中括号,特殊字符). 这个命令与test命令等价,并且出于效率上的考虑,这是一个内建命令.这个命令把它的参数作为比较表达式或者作为文件测试,并且根据比较的结果来返回一个退出状态码(0表示真,1表示假)

3. 在版本2.02的Bash中,引入了 [[ ... ]] 扩展测试命令,因为这种表现形式可能对某些语言的程序员来说更容易熟悉一些.主要[[是一个关键字,并不是一个命令.

   > Bash把[[ $a -lt $b]] 看作一个单独的元素,并且返回一个退出状态码.  
   >
   > (( ... )) 和let ... 结构也能够返回退出状态码,当它们所测试的算术表达式的结果为非零的时候,将返回退出状态码0.

4. if 命令能够测试任何命令,并且不仅仅是中括号中的条件

5. 一个if/then结构可以包含嵌套的比较操作和条件判断操作.

例子7-1 什么是真 

```bash
#! /bin/bash
# 小技巧
# 如果你不能确定一个特定的条件该如何判断,那么就使用if-test结构
echo
echo "Testing \"0\""
if [ 0 ]
then
	echo "0 is true."
else
	echo "0 is false."
fi	# 0为真

echo "Testing \"1\""
if [ 1 ]
then
	echo "1 is true."
else
	echo "1 is false."
fi	# 1为真
echo
echo "Testing \"-1\""
if [ -1 ]
then
	echo "-1 is true."
else
	echo "-1 is false."
fi	# -1为真
echo
echo "Testing \"NULL\""
if [  ]
then
	echo "NULL is true."
else
	echo "NULL is false."
fi	# NULL为假
echo

echo "Testing \"$xyz\""
if [ $xyz ]		# 判断$xyz是否null,这是一个未初始化的变量
then
	echo "Uninitialized variable is true."
else
	echo "Uninitialized variable is flase."
fi		# 未定义的初始化为假
echo

echo "Testing \"-n $xyz\""
if [ -n $xyz ]		# 更加正规的条件检查
then
	echo "Uninitialized variable is true."
else
	echo "Uninitialized variable is flase."
fi		# 未定义的初始化为假
echo

xyz= 	# 初始化了,但是赋null值
echo "Testing \"-n $xyz\""
if [ -n $xyz ]		
then
	echo "Null variable is true."
else
	echo "Null variable is flase."
fi		# null变量为假
echo

# 什么时候"false"为真?

echo "Testing \"false\""
if [ "false" ] # 看起来"false"只不过是一个字符串而已.
then
echo "\"false\" is true." #+ 并且条件判断的结果为真.
else
echo "\"false\" is false."
fi # "false" 为真.

echo

echo "Testing \"\$false\"" # 再来一个, 未初始化的变量.
if [ "$false" ]
then
echo "\"\$false\" is true."
else
echo "\"\$false\" is false."
fi # "$false" 为假.
# 现在, 我们得到了预期的结果.

# 如果我们测试以下为初始化的变量"$true"会发生什么呢?

echo

exit 0

```

> 如果if和then在条件判断的同一行上的话,必须使用分号来结束if表达式.if和then都是关键字.关键字或者命令如果作为表达式的开头,并且如果想在同一行上再写一个新的表达式的话,那么必须使用分号来结束上一句表达式.  
>
> elif是else if的缩写形式.作用是在外部的判断结构中在嵌入一个内部的if/then结构.  
>
> if test condition-true结构与if [ condition-true ]完全相同.左中括号 [ ,是调用test命令的标识,而关闭条件判断用的右中括号, ] , 在if/then机构中并不是严格必须的,但是在新的Bash的新版本中必须要求使用.  
>
> test命令在Bash中是一个内建命令,用来测试文件类型,或者用来比较字符串.

例子7-2 test, /usr/bin/test, [  ] 和 /usr/bin/[ 都是等价命令

```bash
#! /bin/bash
echo
if test -z "$1"
then 
	echo "No command-line arguments."
else
	echo "First command-line arguments $1."
fi

echo 
if /usr/bin/test -z "$1"	# 与内建命令test结果相同
then 
	echo "No command-line arguments."
else
	echo "First command-line arguments $1."
fi

if [ -z "$1" ]
then 
	echo "No command-line arguments."
else
	echo "First command-line arguments $1."
fi

if /usr/bin/[ -z "$1" ]
then 
	echo "No command-line arguments."
else
	echo "First command-line arguments $1."
fi
echo
exit 0
	
```

> [[  ]]结构比[  ]结构更加通用.这是一个扩展的test命令,是从ksh88中引进.  
>
> 在[[和]]之间所有的字符串都不会发生文件名扩展或者单词分割,但是会发生参数扩展和命令替换. 
>
> [[ ... ]]条件判断结构,而不是[ ... ],能够防止脚本的许多逻辑错误.比如 &&, ||, < , > 操作符能够正常存在于[[]]条件判断机构中,但是如果出现在[ ]结构中的话,会报错.
>
> 在if后面也不一定非得是test命令或者是用于条件判断的中括号结构 ([  ] , [[ ]]), "if COMMAND"结构将会返回COMMAND的退出状态码.于此相似,在中括号的条件判断也不一定非的要if不可,也可以使用列表结构.  
>
> (( ))结构扩展并计算一个算术表达式的值.如果表达式的结果为0, 那么返回的退出状态码为1, 或者
> 是"假". 而一个非零值的表达式所返回的退出状态码将为0, 或者是"true". 这种情况和先前所讨论
> 的test命令和[ ]结构的行为正好相反. 

例子7-3 算术测试需要使用 (( ))

```bash
#!/bin/bash
# 算术测试.
# (( ... ))结构可以用来计算并测试算术表达式的结果.
# 退出状态将会与[ ... ]结构完全相反!
(( 0 ))
echo "Exit status of \"(( 0 ))\" is $?." # 1
(( 1 ))
echo "Exit status of \"(( 1 ))\" is $?." # 0

(( 5 > 4 )) # 真
echo "Exit status of \"(( 5 > 4 ))\" is $?." # 0

(( 5 > 9 )) # 假
echo "Exit status of \"(( 5 > 9 ))\" is $?." # 1

(( 5 - 5 )) # 0
echo "Exit status of \"(( 5 - 5 ))\" is $?." # 1

(( 5 / 4 )) # 除法也可以.
echo "Exit status of \"(( 5 / 4 ))\" is $?." # 0

(( 1 / 2 )) # 除法的计算结果 < 1.
echo "Exit status of \"(( 1 / 2 ))\" is $?." # 截取之后的结果为 0.
# 1

(( 1 / 0 )) 2>/dev/null # 除数为0, 非法计算.
# ^^^^^^^^^^^
echo "Exit status of \"(( 1 / 0 ))\" is $?." # 1

# "2>/dev/null"起了什么作用?
# 如果这句被删除会怎样?
# 尝试删除这句, 然后在运行这个脚本.

exit 
```

## 7.2 文件测试符

如果一下条件成立将会返回真.

-e	文件存在

-a	文件存在,效果与-e相同,已弃用

-f	表示这个文件是普通文件

-s	文件大小不为零

-d	表示这是一个目录

-b	表示这是一个块设备(软盘,光驱等等)

-c	表示这是一个字符设备(键盘,modem,声卡等等)

-p	表示文件是一个管道

-h	这是一个符号链接

-L	这是一个符号链接

-S	表示这是一个socket

-t	文件描述符被关联到一个终端设备上.

-r	文件是否具有可读权限

-w	文件是否具有可写权限

-x	文件是否具有可执行权限

-g	set-group-id(sgid)标记被设置到文件或目录上

-u	set-user-id(suid)标记被设置到文件上,对于设置了suid标志的文件,在它的权限列中将会以s表示.

-k	设置粘贴位

> 对于"粘贴位"的一般了解,save-text-mode标志一个文件权限的特殊类型.如果文件设置了这个标志,那么这个文件将会被保存到缓存中,这样可以提高访问速度.粘贴位如果设置在目录中,那么将限制写权限.对于设置了粘贴位的文件或目录,在它们的权限标记列中将会显示t

-O	判断是否是文件拥有者

-G	文件的group-id是否与你相同

-N	从文件上一次被读取到现在为止,文件是否被修改过

f1 -nt f2	文件f1比文件f2新

f1 -ot f2 文件f1比文件f2旧

f1 -et f2 	文件f1和文件f2是相同文件的硬链接

!	"非"--反转上边所有测试的结果.

## 7.3 其他比较操作符

- 整数比较

-eq	等于

-ne	不等于

-gt	大于

-ge	大于等于

-lt	小于

-le	小于等于 if [ "$a" -le "$b" ] 

<	小于(在双括号中使用)	(("$a" < "$b")) 

<=	小于等于(在双括号中使用)

\>	大于(在双括号中使用)

\>=	大于等于(在双括号中使用)

- 字符串比较

=	等于 if [ "$a" = "$b" ] 

==	等于与=等价,==比较操作符在双括号对和单中括号对中行为是不同的

!=	不等于

<	小于,按照ASCII字符进行排序,注意"<"使用在[ ]结构中的时候需要被转义 .

\>	大于,按照ASCII字符进行排序,注意">"使用在[ ]结构中的时候需要被转义 .

-z	字符为null

-n	字符串不为null,当-n使用中括号进行条件测试的时候,必须要把字符串用双引号引用起来.

例子7-5 算术比较和字符串比较

 

```bash
#! /bin/bash
a=4
b=5
echo
if [ "$a" -ne "$b" ]
then
	echo "$a is not equal to $b"
	echo "(arithmetic cpmparison)"
fi

echo
if [ "$a" != "$b" ]
then
	echo "$a is not equal to $b"
	echo "(String comparison)"
fi
# 在这个特定例子中,"-ne" "!="都可以
echo
exit 0
```

例子7-6 检查字符串是否null

```bash
#! /bin/bash
# str-test.sh: 检查null字符串和未引用的字符.
# 如果字符串并没有被初始化, 那么它里面的值未定义.
# 这种状态被称为"null" (注意这与零值不同).
if [ -n $string1 ]
then
	echo "String \"string1\" is not null"
else
	echo "String \"string1\" is null"
fi
echo
if [ -n "$string1" ]
then
	echo "String \"string1\" is not null"
else
	echo "String \"string1\" is null"
fi
echo
if [ $string1 ]
then
	echo "String \"string1\" is not null"
else
	echo "String \"string1\" is null"
fi
echo

string1=initialized
if [ $string1 ]
then
	echo "String \"string1\" is not null"
else
	echo "String \"string1\" is null"
fi
echo
string1="a = b"
if [ $string1 ]
then
	echo "String \"string1\" is not null"
else
	echo "String \"string1\" is null"
fi
echo
exit 0
```

- 逻辑比较

-a	逻辑与 exp1 -a exp2 如果表达式exp1和exp2都为真的话, 那么结果为真 

-o	逻辑或exp1 -a exp2 如果表达式exp1和exp2至少一个为真的话, 那么结果为真 

## 7.4 嵌套的if/then条件测试

通过if/then结构来使用嵌套的条件测试.最终结果和上面使用&&混合比较操作符结果是相同的.



# 8.操作符与相关主题

## 8.1 操作符

- 赋值

变量赋值: 初始化或者修改变量的值.

=	通用赋值操作符,可用于算术和字符串赋值.

- 算术操作符

\+     加法计算

\-	减法计算

\*	乘法计算

/	除法计算

**	幂运算

%	模运算,或者是求余运算

例子8-1 最大公约数

```bash
#!/bin/bash
# gcd.sh: 最大公约数
# 使用Euclid的算法

# 两个整数的"最大公约数" (gcd),
#+ 就是两个整数所能够同时整除的最大的数.

# Euclid算法采用连续除法.
# 在每一次循环中,
#+ 被除数 <--- 除数
#+ 除数 <--- 余数
#+ 直到 余数 = 0.
#+ 在最后一次循环中, gcd = 被除数.
#
# 关于Euclid算法的更精彩的讨论, 可以到
#+ Jim Loy的站点, http://www.jimloy.com/number/euclids.htm.


# ------------------------------------------------------
# 参数检查
ARGS=2
E_BADARGS=65

if [ $# -ne "$ARGS" ]
then
echo "Usage: `basename $0` first-number second-number"
exit $E_BADARGS
fi
# ------------------------------------------------------


gcd ()
{

dividend=$1 # 随意赋值.
divisor=$2 #+ 在这里, 哪个值给的大都没关系.
# 为什么没关系?

remainder=1 # 如果在循环中使用了未初始化的变量,
#+ 那么在第一次循环中,
#+ 它将会产生一个错误消息.

until [ "$remainder" -eq 0 ]
do
let "remainder = $dividend % $divisor"
dividend=$divisor # 现在使用两个最小的数来重复.
divisor=$remainder
done # Euclid的算法

} # Last $dividend is the gcd.


gcd $1 $2

echo; echo "GCD of $1 and $2 = $dividend"; echo


# Exercise :
# --------
# 检查传递进来的命令行参数来确保它们都是整数.
#+ 如果不是整数, 那就给出一个适当的错误消息并退出脚本.

exit 0
```

+=	加-等于(把变量的值增加一个常量然后再把结果赋给变量) 

-= 	减-等于(把变量的值减去一个常量然后再把结果赋给变量) 

*=	乘-等于(把变量的值乘以一个常量然后再把结果赋给变量) 

/= 	除-等于(把变量的值除以一个常量然后再把结果赋给变量) 

%=	取模-等于(先对变量进行模运算, 即除以一个常量取模 ,然后再把结果赋给变量) 

例子 8-2 使用算术操作符

```bash
#!/bin/bash
# 使用10种不同的方法计数到11.

n=1; echo -n "$n "

let "n = $n + 1" # let "n = n + 1" 也可以.
echo -n "$n "


: $((n = $n + 1))
# ":" 是必需的, 因为如果没有":"的话,
#+ Bash将会尝试把"$((n = $n + 1))"解释为一个命令.
echo -n "$n "

(( n = n + 1 ))
# 上边这句是一种更简单方法.
# 感谢, David Lombard, 指出这点.
echo -n "$n "

n=$(($n + 1))
echo -n "$n "

: $[ n = $n + 1 ]
# ":" 是必需的, 因为如果没有":"的话,
#+ Bash将会尝试把"$[ n = $n + 1 ]"解释为一个命令.
# 即使"n"被初始化为字符串, 这句也能够正常运行.
echo -n "$n "

n=$[ $n + 1 ]
# 即使"n"被初始化为字符串, 这句也能够正常运行.
#* 应该尽量避免使用这种类型的结构, 因为它已经被废弃了, 而且不具可移植性.
# 感谢, Stephane Chazelas.
echo -n "$n "

# 现在来一个C风格的增量操作.
# 感谢, Frank Wang, 指出这点.

let "n++" # let "++n" 也可以.
echo -n "$n "

(( n++ )) # (( ++n ) 也可以.
echo -n "$n "

: $(( n++ )) # : $(( ++n )) 也可以.
echo -n "$n "

: $[ n++ ] # : $[ ++n ]] 也可以.
echo -n "$n "

echo

exit 0
```

- 位操作符

>​	位操作符在shell脚本中很少被使用, 它们最主要的用途就是操作和测试从端口或
>者sockets中读取的值. 

<<	左移一位(每次左移都相当于乘以2)

<<=	左移-赋值

\>>	右移一位(每次左移都相当于除以2)

\>>=	右移-赋值

&	按位与

&=	按位与-赋值

|	按位或

|=	按位或-赋值

~	按照反

!	按位非

^	按位异或

^=	按位异或-赋值

&&	与(逻辑)

||	或(逻辑)

例子8-3 使用&&和||进行混合条件测试

```bash
#!	/bin/bash
a=24
b=47
if [ "$a" -eq 24 ] && [ "$b" -eq 47 ]
then
	echo "Test #1 succeeds."
else
	echo "Test #1 fails."
fi
# ERROR: if [ "$a" -eq 24 && "$b" -eq 47 ]
#+ 尝试运行' [ "$a" -eq 24 '
#+ 因为没找到匹配的']'所以失败了.
#
# 注意: if [[ $a -eq 24 && $b -eq 24 ]] 也能正常运行.
# 双中括号的if-test结构要比
#+ 单中括号的if-test结构更加灵活.
# (在第17行"&&"与第6行的"&&"具有不同的含义.)
if [ "$a" -eq 24 ] || [ "$b" -eq 47 ]
then
	echo "Test #1 succeeds."
else
	echo "Test #1 fails."
fi
# -a和-o选项提供了
#+ 一种可选的混合条件测试的方法.

if [ "$a" -eq 24 -a "$b" -eq 47 ]
then
echo "Test #3 succeeds."
else
echo "Test #3 fails."
fi


if [ "$a" -eq 98 -o "$b" -eq 47 ]
then
echo "Test #4 succeeds."
else
echo "Test #4 fails."
fi


a=rhino
b=crocodile
if [ "$a" = rhino ] && [ "$b" = crocodile ]
then
echo "Test #5 succeeds."
else
echo "Test #5 fails."
fi

exit 0
```

&&和||操作符也可以用在算术上下文中. 

- 混杂的操作符

,      逗号操作符

> ​	逗号操作符可以连接两个或多个算术运算.所有的操作都会被运行(可能会有副作用),但是指挥返回最后操作的结果.

## 8.2 数字常量

​	shell脚本在默认情况都是把数字作为10进制数来处理.除非这个数字采用了特殊的标记或者前缀.如果数字以0开头的话那么是8进制数如果数字以0x开头的话那么就是16进制数. 如果数字中间嵌入了#的话, 那么就被认为是BASE#NUMBER形式的标记法(有范围和符号限制). .

例子8-4 数字常量表示法

```bash
#!/bin/bash
# numbers.sh: 几种不同数制的数字表示法.

# 10进制: 默认情况
let "dec = 32"
echo "decimal number = $dec" # 32
# 这没什么特别的.


# 8进制: 以'0'(零)开头
let "oct = 032"
echo "octal number = $oct" # 26
# 表达式结果是用10进制表示的.
# ---------------------------

# 16进制: 以'0x'或者'0X'开头的数字
let "hex = 0x32"
echo "hexadecimal number = $hex" # 50
# 表达式结果是用10进制表示的.

# 其他进制: BASE#NUMBER
# BASE的范围在2到64之间.
# NUMBER的值必须使用BASE范围内的符号来表示, 具体看下边的示例.


let "bin = 2#111100111001101"
echo "binary number = $bin" # 31181

let "b32 = 32#77"
echo "base-32 number = $b32" # 231

let "b64 = 64#@_"
 echo "base-64 number = $b64" # 4031
# 这个表示法只能工作于受限的ASCII字符范围(2 - 64).
# 10个数字 + 26个小写字母 + 26个大写字符 + @ + _


echo

echo $((36#zz)) $((2#10101010)) $((16#AF16)) $((53#1aA))
# 1295 170 44822 3375


# 重要的注意事项:
# ---------------
# 使用一个超出给定进制的数字的话,
#+ 将会引起一个错误.

let "bad_oct = 081"
# (部分的) 错误消息输出:
# bad_oct = 081: value too great for base (error token is "081")
# Octal numbers use only digits in the range 0 - 7.

exit 0 # 感谢, Rich Bartell 和 Stephane Chazelas的指正
```

