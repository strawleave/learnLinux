



***

**不能即时消化的，就给我==详细记==！**

---





[TOC]





















## linux命令帮助获取详解







### 格式

COMMAD option... arguments...

### 内部命令

help COMMAD

hash -r
history -c
history -d 40

### 外部命令

都有一个可执行程序，比如/bin/ls ，位于$PATH
which,whereis     



- COMMAD --help

- man COMMAD

- 信息页 info COMMAD

- 程序自身帮助文档  README INSTALL ChangeLog

  /usr/share/doc/COMMAD-VERSION

- 程序官方文档 Docmenttation

- 发行版官方文档

- Google

#### man手册

- 手册页/usr/share/man
- whatis
- /etc下有MANPATH配置文件 man.config或man_db.conf
- man # COMMAD



> man1: 用户命令
> man2: 系统调用
> man3: C库调用
> man4: 设备文件及特殊文件
> man5: 配置文件格式
> man6: 游戏
> man7: 杂项
> man8: 管理类的命令











































## BASH基础特性



### 命令历史history

环境变量：
HISTSIZE, HISTFILE, HISTFILESIZE, HISTCONTROL

配置文件：
~/.bash_history

命令：
history -c
history -a
history #

> 调用历史中的命令：
> ​	!#: 重复执行第#条指令；
> ​	!!: 
> ​	!string
>
> 调用上一条命令的最后一个参数：
> ​	!$: 
> ​	ESC, .
> ​	Alt+.



### 命令hash



### 命令补全



### 路径补全



### 命令行展开

> ~: 展开为用户的主目录
> ~USERNAME：展开为指定用户的主目录
> {}：可承载一个以逗号分隔的列表，并将其展开为多个路径
> /tmp/{a,b} = /tmp/a, /tmp/b
> /tmp/{tom,jerry}/hi = /tmp/tom/hi, /tmp/jerry/hi

### 命令的执行结果状态

$?

0 成功
1~255 失败



### 命令别名alias

alias NAME='VALUE'
~/.bashrc
/etc/bashrc
ualias cdnet
\cp



### 文件名通配 globbing



### 快捷键

ctrl+a ctrl+e ctrl+u ctrl+k





### 提供了编程环境

1. 变量类型——一旦定义，便限定了数据存储格式、存储空间大小、参与运算种类。

   - 字符型
   - 数值型：整形，浮点型

   ***

   - 强类型：定义变量时必须指定类型，参与的运算必须符合类型要求

   - 弱类型：无需指定类型，默认均为字符型，参与运算时会自动隐式类型转换。

     bash shell属弱类型编程语言。







   根据变量生效范围划分：

   - 本地变量：当前shell有效；

     - 变量赋值  : name="value"

       (1) 直接字串：name="username" (字串中间没有空格的话可以省略引号)

       (2) 变量引用：name="$username"  (加上$符号后表示不再引用username这个字串，而是引用username这个变量)

       (3) 命令引用：name=``COMMAD``  , name=$(COMMAD)  [把命令的**执行结果**赋予name]

       > [root@L code]# filename=$(date +%F-%H-%M-%S)
       > [root@L code]# echo $filename
       > 2019-01-09-14-15-16

     - 变量引用：${name}  $name

       ""：弱引用，其中的变量引用会被替换为变量值；

       ''：强引用，其中的变量引用不会被替换为变量值，而保持原字符串；

   - 环境变量：当前shell以及子shell有效；

     declare -x name=qianli

   - 局部变量：当前shell中某段代码片段（通常指函数中）
   - 位置变量：$1, $2
   - 特殊变量：$? , $0










### bash的配置文件







### bash的算术运算









## BIND DNS







- 程序包

yum list all bind*

rpm -qi bind-libs

rpm -qi bind-utils

> [root@localhost ~]# rpm -ql bind-utils
> /etc/trusted-key.key
> /usr/bin/dig
> /usr/bin/host
> /usr/bin/nslookup
> /usr/bin/nsupdate
> /usr/share/man/man1/dig.1.gz
> /usr/share/man/man1/host.1.gz
> /usr/share/man/man1/nslookup.1.gz
> /usr/share/man/man1/nsupdate.1.gz





- 服务脚本：/etc/rc.d/init.d/named
- 主配置文件：/etc/named.conf , /etc/named.rfc1912.zones , /etc/rndc.key

> rndc: remote name domain controller，默认与bind安装在同一主机，且只能通过127.0.0.1来连接named进程；提供辅助性的管理功能；
> 953/tcp

- 解析库文件：/var/named/ZONE_NAME.ZONE





## 文本处理三剑客





### grep

- grep [OPTIONS] PATTERN [FILE...]
  ​	-v 不匹配的
  ​	-i 忽略大小写
  ​	-o 匹配的
  ​	-A -B -C 前后个#行
  ​	-E

- 基本正则表达式元字符

  pattern要是出现元字符，要用引号引起来。

  1. 字符匹配

     .：  匹配任意单个字符；
     []： 匹配指定范围内的任意单个字符
     [^]：匹配指定范围外的任意单个字符
     [:digit:]、[:lower:]、[:upper:]、[:alpha:]、[:alnum:]、[:punct:]、[:space:]

     eg : grep 's..n' /etc/passwd

  2. 匹配次数

     > *：匹配前面的字符任意次；
     >
     > 贪婪模式
     > .*：任意长度的任意字符；
     > \?：匹配其前面的字符0或1次；即前面的可有可无；
     > \\+：匹配其前面的字符至少1次；
     > \\{m\\}：匹配前面的字符m次；
     > \\{m,n\\}：匹配前面的字符至少m次，至多n次；
     > \\{0,n\\}：匹配前面的字符至多n次；
     > \\{m,\\}：匹配前面的字符至少m次；

     eg:

     grep "x*y"  y前面可以有任意个x

     grep "x.*y"  x开头y结尾

     grep "x\?y"

     grep "[[:alpha:]]\\{3\\}t"  某个字母3次再跟上t

  3. 位置锚定

     > ^：行首锚定；用于模式的最左侧；
     > $：行尾锚定；用于模式的最右侧；
     > ^PATTERN$: 用于模式匹配整行；
     > ^$: 空行；
     > ^[[:space:]]*$
     >
     > \< 或 \b：词首锚定；用于单词模式的左侧；
     > \> 或 \b：词尾锚定；用于单词模式的右侧；
     > \<PATTERN\>：匹配整个单词；

  4. 分组

     grep "\\(xy\\)*ab"







## 进程管理工具

- pstree
- ps