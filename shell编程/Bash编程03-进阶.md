# 9. 变量重游

## 9.1 内部变量

内建变量

​	这些变量将会影响bash脚本的行为

$BASH

​	Bash的二进制程序文件的路径

$BASH_ENV

​	这个环境变量指向一个Bash的启动文件,当一个脚本被调用的时候,这个启动文件将会被读取.

$BASH_SUBSHELL

​	这个变量用来提示子shell的层次.

$BASH_VERSINFO[n]

​	这是一个含有6个元素的数组,它包含了所安装的Bash的版本信息.

$BASH_VERSION

​	安装在系统上的Bash版本号.

$DIRSTACK

​	在目录栈中最顶端的值.(将会受到pushd和popd的影响),这个内建变量与dirs命令相符,但是dirs会显示目录栈的整个内容.

$EDITOR

​	脚本所调用的默认编辑器,通常情况下是vi或者emacs

$EUID

​	"有效"用户ID.不管当前用户被假定成什么用户,这个数都用来表示当前用户的标识号,也可能使用su命令来达到假定的目的. $EUID并不一定与$UID相同.

$FUNCNAME

​	当前函数的名字.

$GLOBIGNORE

​	一个文件名的模式匹配列表,如果在通配(globbing)中匹配到文件包含这个列表中的某个文件,那么这个文件将从匹配到的结果中去掉.

$GROUPS

​	目前用户所属的组.这是一个当前用户的组id的列表(数组),与记列在/etc/passwd文件中内容一样.

$HOME

​	用户的home目录.一般是/home/username

$HOSTNAME

​	hostname放在一个初始化的脚本中,在系统启动的时候分配一个系统的名字.然而,gethostname()函数可以用来设置这个Bash内部变量$HOSTNAME.

$HOSTTYPE

​	主机类型.就像$MACHTYPE,用来识别系统硬件.

$IFS

​	内部域分隔符.这个变量用来决定Bash在解释字符串时如何识别域,或者单词边界.

​	$IFS默认为空白(空格,制表符和换行符),但这是可以修改的.注意$*使用的是保存$IFS中的第一个字符.

​	$IFS处理其他字符与处理空白字符不同. 

​	例子 9-1. $IFS与空白字符 

```bash
#! /bin/bash
# $IFS 处理空白与处理其他字符不同.
output_args_one_per_line()
{
    for arg
    do
    	echo "[$arg]"
    done
}
echo; echo "$IFS=\" \""
echo "---------"
IFS="  "
var=" a   b c   "
output_args_one_per_line $var	# output_args_one_per_line `echo " a b c "`
echo; echo "IFS=:"
echo "---------"
IFS=:
var=":a::b:c:::"
output_args_one_per_line $var
echo
exit 0

```

$IGNOREEOF
​	忽略EOF: 告诉shell在log out之前要忽略多少文件结束符(control-D).
$LC_COLLATE
​	常在.bashrc或/etc/profile中设置, 这个变量用来控制文件名扩展和模式匹配的展开顺序. 如果$LC_COLLATE设置得不正确的话, LC_COLLATE会在文件名匹配(filename globbing)中产生不可预料的结果. 

$LC_CTYPE
​	这个内部变量用来控制通配(globbing)和模式匹配中的字符串解释.
$LINENO
​	这个变量用来记录自身在脚本中所在的行号. 这个变量只有在脚本使用这个变量的时候才有意义,并且这个变量一般用于调试目的. 

$MACHTYPE
​	机器类型 标识系统的硬件. 

$OLDPWD
​	之前的工作目录("OLD-print-working-directory", 就是之前你所在的目录)
$OSTYPE
​	操作系统类型 

$PATH
​	可执行文件的搜索路径, 一般为/usr/bin/, /usr/X11R6/bin/, /usr/local/bin, 等等.当给出一个命令时, shell会自动生成一张哈希(hash)表, 并且在这张哈希表中按照path变量中所列出的路径来搜索这个可执行命令. 路径会存储在环境变量中, $PATH变量本身就一个以冒号分隔的目录列表. 通常情况下, 系统都是在/etc/profile和~/.bashrc中存储$PATH的定义. 

$PIPESTATUS
​	这个数组变量将保存最后一个运行的前台管道的退出状态码. 相当有趣的是, 这个退出状态码和最后一个命令运行的退出状态码并不一定相同. 

​	$PIPESTATUS数组的每个成员都保存了运行在管道中的相应命令的退出状态码. $PIPESTATUS[0]保存管道中第一个命令的退出状态码. $PIPESTATUS[1]保存第二个命令的退出状态码, 依此类推. 

$PPID
​	进程的$PPID就是这个进程的父进程的进程ID(pid). 

$PROMPT_COMMAND
​	这个变量保存了在主提示符$PS1显示之前需要执行的命令 .

$PS1
​	这是主提示符, 可以在命令行中见到它.
$PS2
​	第二提示符, 当你需要额外输入的时候, 你就会看到它. 默认显示">".
$PS3
​	第三提示符, 它在一个select循环中显示 .

$PS4
​	第四提示符, 当你使用-x选项来调用脚本时, 这个提示符会出现在每行输出的开头. 默认显示"+".
$PWD
​	工作目录(你当前所在的目录)
​	这与内建命令pwd作用相同. 

$REPLY
​	当没有参数变量提供给read命令的时候, 这个变量会作为默认变量提供给read命令. 也可以用于select菜单, 但是只提供所选择变量的编号, 而不是变量本身的值. 

$SECONDS
​	这个脚本已经运行的时间(以秒为单位). 

$SHELLOPTS
​	shell中已经激活的选项的列表, 这是一个只读变量. 

$SHLVL
​	Shell级别, 就是Bash被嵌套的深度. 如果是在命令行中, 那么$SHLVL为1, 如果在脚本中那么$SHLVL为2.
$TMOUT
​	如果$TMOUT环境变量被设置为非零值time的话, 那么经过time秒后, shell提示符将会超时. 这将会导致登出(logout). 

例子 9-2. 定时输入 

```bash
#! /bin/bash
# timed-input.sh
# TMOUT=3
TIMELIMIT=3	# 
PrintAnswer()
{
    if [ "$answer" = TIMEOUT ]
    then
    	echo $answer
    else
    	echo "Your favorite veggie is $answer"
    	kill $!	# 不在需要后台运行Timeron函数了,kill掉
    			# $!变量是上一个后台运行的作业的PID
    fi
}

TimerOn()
{
    sleep $TIMELIMIT && kill -s 14 $$ &
    # 等待3秒,然后给脚本发送一个信号
}

Int14Vector()
{
    answer="TIMEOUT"
    PrintAnswer
    exit 14
}

trap Int14Vector 14 # 定时中断(14)会暗中给定时间限制.
echo "What is your favorite vegetable "
TimerOn
read answer
PrintAnswer
exit 0
```

例子 9-3. 再来一个, 定时输入 

```bash
#! /bin/bash
# timeout.sh

INTERVAL=5	#超时间隔
timedout_read(){
    timeout=$1
    varname=$2
    old_tty_settings=`stty -g`
    stty -icanon min 0 time ${timeout}0
    eval read $varname
    stty "$old_tty_settings"
}
echo; echo -n "What's your name?Quick"
timedout_read $INTERVAL your_name
# 这种方法可能并不是在每种终端类型上都可以正常使用的.
# 最大的超时时间依赖于具体的中断类型.
#+ (通常是25.5秒).
echo
if [ ! -z "$your_name" ]
then
	echo "Your name is $your_name."
else
	echo "Timed out."
fi
echo
# 这个脚本的行为可能与脚本"timed-input.sh"的行为有些不同.
# 每次按键, 计时器都会重置.
exit 0
```

可能最简单的办法就是使用-t选项来read了. 

例子 9-4. 定时read 

```bash
#! /bin/bash
# t-out.sh
TIMELIMIT=4	
read -t $TIMELIMIT variable <&1
echo
if [ -z "$variable" ]
then
	echo "Timed out, variable still unset."
else
	echo "variable = $variable"
fi
exit 0
```

$UID
​	用户ID号 当前用户的用户标识号, 记录在/etc/passwd文件中
​	这是当前用户的真实id, 即使只是通过使用su命令来临时改变为另一个用户标识, 这个id也不会被改变. $UID是一个只读变量, 不能在命令行或者脚本中修改它, 并且和id内建命令很相像. 

例子 9-5. 我是root么? 

```bash
#! /bin/bash
# am-i-root.sh
ROOT_UID=0	# root的$UID为0
if [ "$UID" -eq "$ROOT_UID" ]
then
	echo "You are root."
else
	echo "You are just an ordinary user (but mom loves you just the same)."
fi
exit 0

# ============================================= #
# 下边的代码不会执行, 因为脚本在上边已经退出了.

# 下边是另外一种判断root用户的方法:

ROOTUSER_NAME=root

username=`id -nu` # 或者... username=`whoami`
if [ "$username" = "$ROOTUSER_NAME" ]
then
echo "Rooty, toot, toot. You are root."
else
echo "You are just a regular fella."
fi
```

位置参数
​	$0, $1, $2, 等等. 位置参数, 从命令行传递到脚本, 或者传递给函数, 或者set给变量 

$#
​	命令行参数 [2] 或者位置参数的个数
$*
​	所有的位置参数都被看作为一个单词."$**"必须被引用起来.
$@
​	与$*相同, 但是每个参数都是一个独立的引用字符串, 这就意味着, 参数是被完整传递的, 并没有被解释或扩展. 这也意味着, 参数列表中每个参数都被看作为单独的单词.当然, "$@"应该被引用起来.

例子 9-6. arglist: 通过$*和$@列出所有的参数 

```bash
#! /bin/bash
# arglist.sh
# 多使用几个参数来调用这个脚本
E_BADARGS=65
if [ ! -n "$1" ]
then
	echo "Usage:`basename $0` argument1 argument2 etc."
	exit $E_BADARGS
fi

echo
index=1 	#起始计数
echo "Listing args with \"\$*\":"
for arg in "$*"
do 
	echo "Arg #$index = $arg"
	let "index+=1"
done	#$* 将所有的参数看成一个单词
echo "Entire arg list seen as single word."
echo
index=1 # 重置计数(译者注: 从1开始).
# 如果你写这句会发生什么?

echo "Listing args with \"\$@\":"
for arg in "$@"
do
echo "Arg #$index = $arg"
let "index+=1"
done # $@ 把每个参数都看成是单独的单词.
echo "Arg list seen as separate words."

echo

index=1 # 重置计数(译者注: 从1开始).

echo "Listing args with \$* (unquoted):"
for arg in $*
do
echo "Arg #$index = $arg"
let "index+=1"
done # 未引用的$*将会把参数看成单独的单词.
echo "Arg list seen as separate words."

exit 0
```

$*和$@中的参数有时候会表现出不一致而且令人迷惑的行为, 这都依赖于$IFS的设置. 

例子 9-7. $*和$@的不一致的行为 

```bash
#! /bin/bash

# 内部Bash变量"$*"和"$@"的古怪行为,
#+ 都依赖于它们是否被双引号引用起来.
# 单词拆分与换行的不一致的处理.

set -- "First one" "second" "third:one" "" "Fifth: :one"
# 设置这个脚本的参数, $1, $2, 等等.
echo
echo 'IFS unchanged, using "$*"'
c=0
for i in "$*"	# 引用起来
do echo "$((c+=1)) : [$i]"
done
echo ---
echo 'IFS unchanged, using "$*"'
c=0
for i in $*	# 未起来
do echo "$((c+=1)) : [$i]"
done
echo ---
echo 'IFS unchanged, using "$@"'
c=0
for i in "$@"
do echo "$((c+=1)): [$i]"
done
echo ---

echo 'IFS unchanged, using $@'
c=0
for i in $@
do echo "$((c+=1)): [$i]"
done
echo ---

IFS=:
echo 'IFS=":", using "$*"'
c=0
for i in "$*"
do echo "$((c+=1)): [$i]"
done
echo ---

echo 'IFS=":", using $*'
c=0
for i in $*
do echo "$((c+=1)): [$i]"
done
echo ---

var=$*
echo 'IFS=":", using "$var" (var=$*)'
c=0
for i in "$var"
do echo "$((c+=1)): [$i]"
done
echo ---

echo 'IFS=":", using $var (var=$*)'
c=0
for i in $var
do echo "$((c+=1)): [$i]"
done
echo ---

var="$*"
echo 'IFS=":", using $var (var="$*")'
c=0
for i in $var
do echo "$((c+=1)): [$i]"
done
echo ---

echo 'IFS=":", using "$var" (var="$*")'
c=0
for i in "$var"
do echo "$((c+=1)): [$i]"
done
echo ---86
echo 'IFS=":", using "$@"'
c=0
for i in "$@"
do echo "$((c+=1)): [$i]"
done
echo ---

echo 'IFS=":", using $@'
c=0
for i in $@
do echo "$((c+=1)): [$i]"
done
echo ---

var=$@
echo 'IFS=":", using $var (var=$@)'
c=0
for i in $var
do echo "$((c+=1)): [$i]"
done
echo ---

echo 'IFS=":", using "$var" (var=$@)'
c=0
for i in "$var"
do echo "$((c+=1)): [$i]"
done
echo ---

var="$@"
echo 'IFS=":", using "$var" (var="$@")'
c=0
for i in "$var"
do echo "$((c+=1)): [$i]"
done
echo ---

echo 'IFS=":", using $var (var="$@")'
c=0
for i in $var
do echo "$((c+=1)): [$i]"
done

echo

# 使用ksh或者zsh -y来试试这个脚本.

exit 0
```

$@与$*中的参数只有在被双引号引用起来的时候才会不同. 

例子 9-8. 当$IFS为空时的$*和$@ 

```bash
#! /bin/bash
# 如果$IFS被设置, 但其值为空,
#+ 那么"$*"和"$@"将不会像期望的那样显示位置参数.
mecho()		# 打印位置参数
{
    echo "$1,$2,$3"
}
IFS=""	#设置IFS为空
set a b c
mecho "$*"
mecho $*
mecho $@
mecho "$@"
# 当$IFS值为空时, $*和$@的行为依赖于
#+ 正在运行的Bash或者sh的版本.
# 因此在脚本中使用这种"特性"是不明智的.
exit 0
```

其他的特殊参数
$-
​	传递给脚本的标记(使用set命令). 

$!
​	运行在后台的最后一个作业的PID(进程ID) 

$_
​	这个变量保存之前执行的命令的最后一个参数的值. 

例子 9-9. 下划线变量 

```bash
#! /bin/bash
echo $_				# /bin/bash,只是调用/bin/bash来运行这个脚本
du > /dev/null		
echo $_				# du
ls -al > /dev/null	
echo $_				# -al (这是最后的参数)
:
exit $_				# :
```

$?
​	命令, 函数, 或者是脚本本身的退出状态码
$$
​	脚本自身的进程ID. $$变量在脚本中经常用来构造"唯一的"临时文件名 .

## 9.2 操作字符串

