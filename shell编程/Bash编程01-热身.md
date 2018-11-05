# 第一部分 热身

shell是一个命令解释器。是介于操作系统内核与用户之间的一个绝缘层。准确的说，它也是能力很强的计算机语言，一种shell程序，同时也被称为一种脚本语言。它是非常容易使用的工具，它可以通过将系统调用，公共程序，工具，和编译过的二进制程序"粘合"在一起来建立应用。事实上，所有的UNIX命令和工具再加上公共程序，对shell脚本来说，都是可调用的。

## 为什么使用shell编程？

没有程序语言是完美的。甚至没有一个唯一最好的语言，只有对于特定目的，比较适合和不适合的程序语言----Herbert Mayer  
对于任何适当精通一些系统管理的知识的人来说，掌握shell脚本知识都是最基本的，即使这些人可能不打算真正的编写一些脚本。  
Shell脚本遵循典型的UNIX哲学，就是把大的复杂的工程分成小规模的子任务，并且把这些部件和工具组合起来。

### 什么时候不适合使用shell脚本

* 资源密集型任务，尤其在需要考虑效率时（比如排序、hash等等）
* 需要处理大任务的数学操作，尤其是浮点运算，精确运算，或者复杂的算术运算（这种情况一般使用C++或者FORTRAN来处理）
* 有跨平台移植需要（一般使用C或Java）
* 复杂的应用，必须使用结构化编程的时候（需要变量的类型检查，函数原型等等）
* 至关重要的应用
* 对于安全有很高要求的任务，比如防止入侵、破解、恶意破坏等等
* 工程的每个组成部分之间，需要连锁的依赖性
* 需要大规模的文件操作（Bash受限于顺序地进行文件访问，而且只能使用这种笨拙的效率低下的一行接一行的处理方式）
* 需要多维数组的支持
* 需要数据结构的支持，比如链表或数组等数据结构
* 需要产生或操作图形化界面GUI
* 需要直接操作系统硬件
* 需要I/O或者socket接口
* 需要使用库或者遗留下来的旧代码的接口
* 个人的，闭源的应用（shell脚本就是把代码放在文本文件中）

Base是"Bourne-Again shell"首字母的缩写，也是Stephen Bourne的经典的Bourne shell的一个双关语。对于所有的UNIX/Linux上的shell脚本来说，Bash已经称为了事实上的标准了。

## 带着一个Sha-Bang出发（Sha-Bang指的是#!）

一个最简单的例子中，一个shell脚本其实就是将一堆系统命令列在一个文件中。  
例子2-1 清除

    # 清除
    # 当然要使用root身份来运行这个脚本.

    cd /var/log
    cat /dev/null > messages
    cat /dev/null > wtmp
    echo "Logs cleaned up."

例子2-2 清除：一个改良的清除脚本

    #! /bin/bash
    # 一个Bash脚本的正确的开头部分.

    # Cleanup,版本2
    # 当然要使用root身份来运行
    # 在此处插入代码，来打印错误消息，并且在不是root身份时候退出

    LOG_DIR=/var/log
    # 如果使用变量，当然比把代码写死的好
    cd $LOG_DIR
    cat /dev/null > messages
    cat /dev/null > wtmp

    echo "Logs cleaned up."
    exit # 这个命令式一种正确并且合适的退出脚本的方法。

例子2-3清除：一个增强的和广义的删除logfile的脚本

    #! /bin/Bash
    # 警告:
    # -----
    # 这个脚本有好多特征,
    #+ 这些特征是在后边章节进行解释的.
    # 大概是进行到本书的一半的时候,
    #+ 你就会觉得它没有什么神秘的了.
    LOG_DIR=/var/log
    ROOT_UID=0  # $UID=0的时候，用户才具有root用户权限
    LINES=60    # 默认的保存行数
    E_XCD=66    # 不能修改目录
    E_NOTROOT=67  # 非root用户将以error退出

    #　当然要使用root用户来运行
    if [ "$UID" -ne "$ROOT_UID" ]
    then
      echo "Must be root to run this script"
      exit $E_NOTROOT
    fi

    # 测试是否有命令行参数（非空）
    if [ -n "$1" ]
    then
      lines=$1
    else
      lines=$LINES  # 默认，如果不在命令行中指定
    fi

    # Stephane Chazelas 建议使用下边
    #+ 的更好方法来检测命令行参数.
    #+ 但对于这章来说还是有点超前.
    #
    # E_WRONGARGS=65 # 非数值参数(错误的参数格式)
    #
    # case "$1" in
    # "" ) lines=50;;
    # *[!0-9]*) echo "Usage: `basename $0` file-to-cleanup"; exit $E_WRONGARGS;;
    # * ) lines=$1;;
    # esac
    #
    #* 直到"Loops"的章节才会对上边的内容进行详细的描述.

    cd $LOG_DIR
    if [ `pwd` != "$LOG_DIR" ] # 或者 if[ "$PWD" != "$LOG_DIR" ]
    then
      echo "Can't change to $LOG_DIR"
      exit $E_XCD
    fi  #在处理log file之前，在确认一遍当前目录是否正确

    # 更有效率的做法是:
    #
    # cd /var/log || {
    # echo "Cannot change to necessary directory." >&2
    # exit $E_XCD;
    # }

    tail -$lines messages > mesg.temp # 保存log file消息的最后部分
    mv mesg.temp messages             # 变为新的log目录

    # cat /dev/null > messages
    # 不在需要了，使用上边的方法更安全
    cat /dev/null > wtmp #  ': > wtmp' 和 '> wtmp'具有相同的作用
    echo "Logs cleaned up."

    exit 0
    #  退出之前返回0
    #+ 返回0表示成功


注意，在每个脚本开头都使用sha-bang（#!），这意味着告诉系统这个文件的执行需要指定一个解释器。#! 实际上一个2字节的魔法数字，这是指定一个文件类型的特殊标记，在这种情况下，指定就是一个可执行的脚本。   
在sha-bang之后接着是一个路径名。这个路径名就是解释脚本中命令的解释程序所在的路径。可以是一个shell，也可能式一个程序语言，或者命令程序。  

    #! /bin/sh
    #! /bin/bash
    #! /usr/bin/perl
    #! /usr/bin/tcl
    #! /bin/sed -f
    #! /usr/awk -f

注意”sha-bang"后面给出的路径名称必须要正确，否则将会出现一个错误信息。
- 具有unix味道的脚本需要一个4字节的魔法数字，在！后边需要一个空格
- 脚本中#!所在的行最重要的任务是告诉系统脚本是使用哪种命令的解释器。如果脚本中还有其他#!行，那么bash将会把他看成一个一般的注释行。

## 调用一个脚本

编写完脚本之后，使用sh scriptname或者bash scriptname来调用这个脚本。更方便的方法是让脚本本身具有可执行权限，通过chmod命令修改。
