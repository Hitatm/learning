## 系统学习Linux Command Line Learning
左键复制，中键粘贴
cd -; cd ~username
>file　清空文件
cmdline ＆>file = cmdline > file 2>&1
echo $((2**3)) = 8 幂运算
touch {1..5}.txt
printenv查看有效变量
echo $(cal) 和　echo "$(cal)"的不同在于双引号之中的空白字符将会保留，不加双引号，其中的空白字符只保留一个．
shell命令行的快捷高级操作：
1. ctrl+t exchange
2. ctrl+f forward移动
3. ctrl+b backward移动
4. ctrl+k 光标后全部删除
5. ctrl+u 光标前全部删除
6. alt+d 删除当前光标后的词
7. alt+backspace 删除当前光标前的词
8. ctrl+y 粘贴刚才删除的
9. ctrl+p,ctrl+n 向上历史命令，向下历史命令
##
表11-1: 进程状态
状态  含义
R   运行中。这意味着，进程正在运行或准备运行。
S   正在睡眠。进程没有运行，而是，正在等待一个事件， 比如说，一个按键或者网络分组。
D   不可中断睡眠。进程正在等待 I/O，比方说，一个磁盘驱动器的 I/O。
T   已停止. 已经指示进程停止运行。稍后介绍更多。
Z   一个死进程或“僵尸”进程。这是一个已经终止的子进程，但是它的父进程还没有清空它。 （父进程没有把子进程从进程表中删除）
<   一个高优先级进程。这可能会授予一个进程更多重要的资源，给它更多的 CPU 时间。 进程的这种属性叫做 niceness。具有高优先级的进程据说是不好的（less nice）， 因为它占用了比较多的 CPU 时间，这样就给其它进程留下很少时间。
N   低优先级进程。 一个低优先级进程（一个“nice”进程）只有当其它高优先级进程被服务了之后，才会得到处理器时间。


top - 12:33:58 up 1 day, 17:54,  2 users,  load average: 0.08, 0.13, 0.09
Tasks: 231 total,   1 running, 229 sleeping,   0 stopped,   1 zombie
%Cpu(s):  3.3 us,  0.9 sy,  0.0 ni, 95.6 id,  0.0 wa,  0.0 hi,  0.3 si,  0.0 st
KiB Mem:   7876508 total,  3577864 used,  4298644 free,   352196 buffers
KiB Swap:  7905276 total,        0 used,  7905276 free.  1214544 cached Mem


jobs ; fg %n ;


umask 0002
export HISTCONTROL=ignoredups
export HISTSIZE=1000
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'

PS1 变量可以设置提示符[here](http://billie66.github.io/TLCL/book/chap14.html)
PS1='\[\033[s\033[0;0H\033[0;41m\033[K\033[1;33m\t\033[0m\033[u\]<\u@\h \W>\$ '
export PS1

包管理工具 发行版 	底层工具 	上层工具
Debian-Style 	dpkg 	apt-get, aptitude
Fedora, Red Hat Enterprise Linux, CentOS 	rpm 	yum

底层软件包安装命令 风格 	命令
Debian 	dpkg --install package_file
Red Hat 	rpm -i package_file

软件包删除命令 风格 	命令
Debian 	apt-get remove package_name
Red Hat 	yum erase package_name

列出所安装的软件包命令 风格 	命令
Debian 	dpkg --list
Red Hat 	rpm -qa

查看软件包信息命令 风格 	命令
Debian 	apt-cache show package_name
Red Hat 	yum info package_name



包文件识别命令 风格 	命令
Debian 	dpkg --search file_name
Red Hat 	rpm -qf file_name
查找安装了某个文件的软件包 
例如：在 Red Hat 系统中，查看哪个软件包安装了/usr/bin/vim 这个文件
rpm -qf /usr/bin/vim


命令	意思
ftp fileserver	唤醒 ftp 程序，让它连接到 FTP 服务器，fileserver。
anonymous	登录名。输入登录名后，将出现一个密码提示。一些服务器将会接受空密码， 其它一些则会要求一个邮件地址形式的密码。如果是这种情况，试着输入 “user@example.com”。
cd pub/cd_images/Ubuntu-8.04	跳转到远端系统中，要下载文件所在的目录下， 注意在大多数匿名的 FTP 服务器中，支持公共下载的文件都能在目录 pub 下找到
ls	列出远端系统中的目录。
lcd Desktop	跳转到本地系统中的 ~/Desktop 目录下。在实例中，ftp 程序在工作目录 ~ 下被唤醒。 这个命令把工作目录改为 ~/Desktop
get ubuntu-8.04-desktop-i386.iso	告诉远端系统传送文件到本地。因为本地系统的工作目录 已经更改到了 ~/Desktop，所以文件会被下载到此目录。
bye	退出远端服务器，结束 ftp 程序会话。也可以使用命令 quit 和 exit

find ~ \( -type f -not -perm 0600 \) -or \( -type d -not -perm 0700 \)
 find 命令的逻辑操作符
 操作符	描述
 -and	如果操作符两边的测试条件都是真，则匹配。可以简写为 -a。 注意若没有使用操作符，则默认使用 -and。
 -or	若操作符两边的任一个测试条件为真，则匹配。可以简写为 -o。
 -not	若操作符后面的测试条件是真，则匹配。可以简写为一个感叹号（!）。
 ()	把测试条件和操作符组合起来形成更大的表达式。这用来控制逻辑计算的优先级。 默认情况下，find 命令按照从左到右的顺序计算。经常有必要重写默认的求值顺序，以得到期望的结果。 即使没有必要，有时候包括组合起来的字符，对提高命令的可读性是很有帮助的。注意 因为圆括号字符对于 shell 来说有特殊含义，所以在命令行中使用它们的时候，它们必须 用引号引起来，才能作为实参传递给 find 命令。通常反斜杠字符被用来转义圆括号字符。


通过把末尾的分号改为加号，就激活了 find 命令的一个功能，把搜索结果结合为一个参数列表， 然后用于所期望的命令的一次执行。再看一下之前的例子，这个例子中：

 find ~ -type f -name 'foo*' -exec ls -l '{}' +
 执行带有 –show–limits 选项 的 xargs 命令，来查看命令行的最大值

 find 命令提供的 -print0 行为， 则会产生由 null 字符分离的输出，并且 xargs 命令有一个 –null 选项，这个选项会接受由 null 字符 分离的输入。这里有一个例子：

 find ~ -iname ‘*.jpg’ -print0	xargs –null ls -l
 使用这项技术，我们可以保证所有文件，甚至那些文件名中包含空格的文件，都能被正确地处理。
