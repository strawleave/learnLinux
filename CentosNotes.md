



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











## Linux的文件系统

- 所有文件从根开始，并不意味着linux系统就不用分区。为了实现多个文件系统独立管理，一样需要分区。但是，分区完成后，不能独立被访问，而应该与根一起被访问。

- 对任何一个操作系统来讲，最关键的是内核。内核其实也是一个应用程序，当被加载完以后，它自己不提供用户可访问的文件，也不是用户可直接使用的有用的进程，所以额外的，内核必须启用很多外部命令，包括shell程序很多GUI或Client接口等等。那么这些应用程序放在什么地方？某一分区之上。但这么多分区，内核是识别哪一个呢？为了避免选择上的困难，一般无论分为多少个分区，都有一个系统盘，给内核启动完以后第一个加载。

- 当内核启动完以后，为了启用各种外围的其他程序，内核会自行在自己的工作空间中，设置一个文件系统，称为 / ,然后把系统分区上的所有文件，关联到/上面，

  某一分区上的目录，作为另外一个分区的访问入口。

- 分区是为了区分系统盘和数据盘(软件安装盘)，日后重装系统只格系统盘足矣,而其他分区所安装的程序能正常使用。

- 既然是系统盘，就有固定的位置存放固定的一类文件。/etc, /usr, /var, /root, /home

- LBS组织，Linux标准库，当中有一个标准：FHS，FileSystem Herrache Standard, 



### 根文件系统(rootfs)

- /boot : 存放引导文件：内核文件(vmlinuz)，引导加载器(bootloader,grub)

  一般来讲是一个独立的分区，是在/上创建boot目录，然后把一个独立的分区挂载到此目录。（如何关联，为什么关联？）

- /bin: 供所有用户使用的基本命令，因为是OS启动即会用到的程序，所以不能关联独立分区。

- /sbin: 管理类的基本命令，不能关联至独立分区，因为是OS启动即会用到的程序。

- /lib: 基本共享库文件，以及内核模块文件(/lib/modules)；

- /lib64: 64位系统所用，放的库文件比lib多得多。

- /etc: 有些应用程序的选项非常之多，而且需要同时指定，通常不会在命令行通过option指定，而是通过读取配置文件来实现。而配置文件（大多数都是纯文本文件）都放/etc目录。

- /home/USERNAME: 普通用户家目录

- /root: 管理员家目录

- /media: 便携式移动设备挂载点,cdrom,usb;

- /mnt: 临时文件系统挂载点；

- /dev: 特殊文件(比如软设备/dev/null,是软件所模拟出来的特殊文件)以及设备文件存放位置。

  b: block device，随机访问，随自己的意愿任意访问
  c: character device，线性访问，有先后顺序

- /opt: 第三方应用程序的安装位置，系统装完后一般都是空的

- /srv: 系统上运行的服务用到的数据，很显然这些服务都是自行管理的，我们很少打交道。

- /tmp: 存放临时文件

- /usr: universal shared read-only data ==只读：已经存放的文件只读==

   通常是被关联到独立分区的目录，系统刚装完后，该目录一般很大，因为usr主要存放除了bin,sbin下的那些基本命令程序以外的其他命令程序、以及诸多用户所用到的只读资源文件和共享资源文件。

  - bin,sbin: 保证系统拥有完整功能而提供的应用程序,而/bin只是保证系统基本运行

  - llib,lib64

  - include: C程序的头文件(header files)

  - share: 结构化的独立数据，如doc, man等

  - local: 第三方应用程序的安装位置（取代了早期的/opt），是可以关联至独立分区的。

    bin, sbin, lib, lib64, etc, share

- /var: variable data files 存放一些经常发生变化的数据文件，也可以关联至独立分区

  var也有自己的层级结构，它必须拥有以下子目录：

  - cache:应用程序缓存数据目录；
  - lib: 记录应用程序处于那种状态；
  - local: 为/usr/local下的应用程序存储可变数据；
  - lock:应用程序的锁文件；
  - log: 日志目录及文件；
  - opt: 专用于为/opt下的应用程序存储可变数据；
  - run: 运行中的进程相关的数据；通常用于存储进程的pid文件；
  - spool: 应用程序数据池；
  - tmp: 保存系统两次重启之间产生的临时数据；

- /proc: 伪文件系统，虚拟文件系统，用于输出内核与进程相关信息。内核中的很多接口都是参数，不是文件，进程所输出的接口也是一些状态信息，是参数不是文件，程序员经常需要看这些信息，所以Linux通过虚拟文件系统，把本来不像文件的内容做得像文件一样，我们可以像访问文件一样访问它们。系统调优大多数是修改proc下某一目录的某一文件的内容，这些内容相当于内核的参数，修改了参数就相当于调整了内核的工作特性。

- /sys: 伪文件系统，用于输出当前系统上硬件设备相关信息的虚拟文件系统；

- lost+found: ext系列的文件系统，默认格式化后会产生的路径。

- /selinux: security enhanced Linux  selinux相关的安全策略等信息的存储位置；

### 应用程序的组成部分



























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





2. 变量种类

   根据变量生效范围划分：

   - 本地变量：当前shell有效；

     - 变量赋值  : name="value"

       (1) 直接字串：name="username" (字串中间没有空格的话可以省略引号)

       (2) 变量引用：name="$username"  (加上$符号后表示不再引用username这个字串，而是引用username这个变量)

       (3) 命令引用：name=``COMMAD``  , name=$(COMMAD)  [把命令的**执行结果**赋予name]

       > [root@L code]# filename=$(date +%F-%H-%M-%S)
       > [root@L code]# echo $filename
       > 2019-01-09-14-15-16

       注意：假如对应的命令的执行结果又空格，则需用引号引起来   name="$(COMMAD)"

       ```shell
       [root@L code]# vim linecount.sh 
       #!/bin/bash
       linecount="$(wc -l $1 | cut -d' ' -f1)"
       echo "$1 has $linecount lines"
       ```

       

     - 变量引用：${name}  $name

       ""：弱引用，其中的变量引用会被替换为变量值；

       ''：强引用，其中的变量引用不会被替换为变量值，而保持原字符串；

     - 显示所有已定义的变量 set    销毁变量  unset name      [不用加$]

   - 环境变量：当前shell以及子shell有效；

     - 声明赋值：

       (1) declare -x name=qianli

       (2) export name=VALUE

     - 变量引用： $name  ${name}

     - 显示所有环境变量： export   env   printenv

     - 销毁变量： unset name

     - 只读变量：常量

       (1)  declare -r name

       (2)  readonly name

   - 局部变量：当前shell中某段代码片段（通常指函数中）

   - 位置变量：$1, $2,   传递所有参数：$*(把所有参数当做一个字符串),$@(每一个参数当做一个独立的字符串),  $# 参数的个数

     ```shell
     [root@L code]# ./posvar.sh qianli yizui gufei
     $1:qianli
     $2:yizui
     命令本身 $0:./posvar.sh
     $*:qianli yizui gufei
     $@:qianli yizui gufei
     有几个参数 $#:3
     ```

     

   - 特殊变量：$? , $0









### bash的配置文件

以生效范围划分：

1. 全局配置
   - /etc/profile , /etc/profile.d/*.sh
   - /etc/bashrc
2. 个人配置
   - ~/.bash_profile
   - ~/.bashrc

按功能划分：

> shell登录：
> 交互式登录：
> 直接通过终端输入账号密码登录；
> 使用“su - UserName”或“su -l UserName”切换的用户
>
> /etc/profile --> /etc/profile.d/*.sh --> ~/.bash_profile --> ~/.bashrc --> /etc/bashrc
>
> 非交互式登录：
> su UserName
> 图形界面下打开的终端
> 执行脚本
>
> ~/.bashrc --> /etc/bashrc --> /etc/profile.d/*.sh

1. profile类：为交互式shell提供配置。用于定义环境变量或运行命令或脚本

   - /etc/profile , /etc/profile.d/*sh , ~/bash_profile

2. bashrc类：非交互。定义命令别名或本地变量。

   - /etc/bashrc , ~/.bashrc

3. 先引用后赋值：

   export PATH=$PATH:/usr/local/bin



### bash的算术运算

1. 实现算数运算

   (1) let var=算术表达式
   (2) var=$[算术表达式]
   (3) var=$((算术表达式))
   (4) var=$(expr arg1 arg2 arg3 ...)

2. 增强型赋值

   - count=$[$count+1]

   - let count+=1
   - let count++  (自增1)

3. 练习：

   ```shell
   [root@L code]# cat useridsum.sh 
   #!/bin/bash
   userid1=$(head -n 10 /etc/passwd | tail -n 1 | cut -d: -f3)
   userid2=$(head -n 20 /etc/passwd | tail -n 1 | cut -d: -f3)
   useridsum=$[$userid1+$userid2]
   echo $useridsum
   [root@L code]# cat spacelinecount.sh 
   #!/bin/bash
   space1=$(grep "^[[:space:]]*$" $1 | wc -l)
   space2=$(grep "^[[:space:]]*$" $2 | wc -l)
   echo "The sum of space line: $[$space1+$space2]"
   ```



### bash的条件测试

1. 测试命令：

   test EXPRESSION
   [ EXPRESSION ]
   [[ EXPRESSION ]]

2. 测试类型

   - 数值测试(数值比较)

     > -gt: 是否大于；
     > -ge: 是否大于等于；
     > -eq: 是否等于；
     > -ne: 是否不等于；
     > -lt: 是否小于；
     > -le: 是否小于等于；

   - 字符串测试

     > ==：是否等于；
     >
     > : 是否大于；
     > <: 是否小于；
     > !=: 是否不等于；
     > =~: 左侧字符串是否能够被右侧的PATTERN所匹配；
     > Note: 此表达式一般用于[[  ]]中；
     > -z "STRING"：测试字符串是否为空，空则为真，不空则为假；
     > -n "STRING"：测试字符串是否不空，不空则为真，空则为假；
     >
     > Note：用于字符串比较时的用到的操作数都应该使用引号；

   - 文件测试

### bash自定义退出状态码

- $?  ： 0 成功； 1~255 失败
- exit [n]  ：  自定义退出状态码 ，遇exit命令，脚本立即终止
- 未给脚本指定退出状态码，则取决于最后一条命令的状态码





## DNS and BIND



### DNS服务介绍

- DNS是一种协议，一种规范，一种概念模型，BIND是DNS协议最著名的实现。[C/S , 53/udp  , 53/tcp]

- 应用层协议，属资源子网那一部分，要借助通信子网完成通信（底层报文从源达到目的方等等），而自己仅负责完成某种特定的功能。

- FQDN：Full  Qualified Domain Name 完全合格域名，完全限定域名

  www.bilibili.com. FQDN  [最后面的.不能省略]

  www 简写的主机名

- 完整的查询请求

  Client --> hosts --> Local Cache --> DNS Server(recursion) --> Sever Cache --> iteration(迭代)

  

### DNS服务器诞生由来

- 早期，互联网主机各自维护自己的Host文件；

- 后来，接入网络中的主机越来越多，IANA专门做了个FTP服务器，任何主机需要使用地址或名称时，就向IANA申请，然后名字和IP的对应关系被保存在FTP上的host文件，各主机计划任务定时去FTP那下载Host文件就行；

- 当host文件记录几何倍增长时，干脆建立了专门负责解析的服务器。

  为了完成通信，系统底层有个库文件，能够在用户通过主机名访问其他主机时，它自己先扮演成客户端，去找一个在本地被配置成DNS的那个主机，扔udp请求去，查询该主机名对应的IP地址，然后才封装通信报文去访问那个IP地址。

  所以，多了一个地址解析服务请求的步骤。这个过程越少消耗时间越好，所以是基于udp协议。

- 向远程DNS服务器请求解析的过程，或多或少是很慢的，可能比查找本地成千上万条host记录快不了多少。所以，DNS服务器采用了一种比较精巧的办法：在服务启动时，会把本地数据库中所有名字和IP的对应关系哈希化，然后保存到内存中。

  哈希计算是指求数据的特征码，比对特征码会更快，哈希计算保存时是是按照哈希桶的方式分单元保存，更便于查找。每次哈希查找所用的时间都是恒等的。

- 但再精巧的办法，单台DNS服务器也架不住上百万的请求。所以，==分片==管理，逐级查找。

***



注：顶级域下注册二级域, ,net.下注册了gmcc.net ,到了三级一般就认为其是个主机名，互联网最常用的是www

正反向解析是两个不同的名称空间，是两棵不同的解析树；所以可以是两台不同的DNS服务器来解析这个域的正反向

***



### 区域解析库

由众多资源记录(Resource Record,RR组成,

#### RR类型：

A(internet Address), 

AAAA(ipv6), 

SOA(Start Of Authority,起始授权记录；一个区域解析库有且仅能有一个SOA记录，而必须为解析库的第一条记录)

PTR(反向)

NS(标识当前区域的DNS服务器)

CNAME(Canonical Name)

MX:　Mail eXchanger，邮件交换器

#### RR格式

name	[TTL]	IN 	rr_type 	value

```
straw.net.	86400	IN	SOA	ns.straw.net.	mail.straw.net.	(
			20190121;序列号
			2H;刷新时间
			10M;重试时间
			1W;过期时间
			1D;否定答案的TTL值
)
straw.net.	IN		NS	ns1.straw.net.
straw.net.	IN		NS	ns2.straw.net.
ns1.straw.net.	IN	A	192.168.64.10
straw.net.	IN		MX	10	mx1.straw.net.
straw.net.	IN		MX	20	mx2.straw.net.
luffy.straw.net.	IN	A	192.168.64.11
sanji.straw.net.	IN	A	192.168.64.12
*.straw.net.		IN	A	192.168.64.13
14.64.168.192.in-addr.arpa	IN	PTR	nami.straw.net.
strawhat.straw.net.	IN	CNAME	luffy.straw.net.
```

- TTL可从全局继承
- @可用于引用当前区域的名字，所以SOA记录里的区域管理员邮箱地址用点代替@
- SOA记录的value值由多部分组成：
  1. 主DNS的FQDN或当前区域的名字；
  2. 邮箱地址；
  3. 主从服务协调属性的定义以及否定答案的统一TTL
- NS和MX记录在后续都应该跟有A记录
- MX记录的value之前有数字，表示优先级，数字越小优先级越高

### 子域授权

每个域的名称服务器，都是通过其上级名称服务器在解析库进行授权

在.net的名称服务器上，解析库添加这样的资源记录，这样的记录叫做粘合记录glue record:

straw.net.	IN	NS	ns1.straw.net.
straw.net.	IN	NS	ns2.straw.net.
ns1.straw.net.	IN	A	1.1.1.1
ns2.straw.net.	IN	A	2.2.2.2



### BIND的安装配置



- dns服务，程序包名bind，程序名进程名named

- 程序包

  yum list all bind*

  bind.x86_64  (主包)
  bind-libs.x86_64
  bind-utils.x86_64

  rpm -qi bind-libs  （库文件）
  rpm -qi bind-utils  （提供测试工具）

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

  rpm -qi bind-chroot 如果软件没装，就用 yum info bind-chroot



- 服务脚本：/etc/rc.d/init.d/named	有服务脚本才可以用services start/stop blabla）

- 主配置文件：/etc/named.conf , /etc/named.rfc1912.zones , /etc/rndc.key

  - rndc: remote name domain controller，默认与bind安装在同一主机，且只能通过127.0.0.1来连接named进程；强大，提供辅助性的管理功能；
    rndc也是个辅助性的服务，所以也必须监听在套接字上，默认使用tcp 953端口；

  - rndc.key就是rndc	去连接named进程时大家共享的密钥，只能在本地执行连接。

  - 为了避免named.conf过长，部分配置分片到named.rfc1912.zones中

    格式：

    options {}
    logging {}
    zone "ZONE_NAME" IN {}

  - 任何服务程序如果期望其能够通过网络被其它主机访问，至少应该监听在一个能与外部主机通信的IP地址上；

    ```shell
    [root@L named]# ss -tunlp | grep :53
    udp    UNCONN     0      0      192.168.64.128:53                    *:*                   users:(("named",pid=14904,fd=515),("named",pid=14904,fd=514))
    udp    UNCONN     0      0      127.0.0.1:53                    *:*                   users:(("named",pid=14904,fd=513),("named",pid=14904,fd=512))
    tcp    LISTEN     0      10     192.168.64.128:53                    *:*                   users:(("named",pid=14904,fd=22))
    tcp    LISTEN     0      10     127.0.0.1:53                    *:*                   users:(("named",pid=14904,fd=21))
    ```

    


​    

- 解析库文件：/var/named/ZONE_NAME.ZONE

  - 可以为多个区域提供解析,即/var/named目录下有多个.zone文件；

  - 必须要有根区域文件named.ca ，这样遇到不会解析的域名才能去请求根；

  - 应该有两个或以上(假如ipv6)的解析库，实现localhost和127.0.0.1的互相解析;

  - 主要有资源记录组成，编辑完之后检查：

    (1)named-checkconf

    (2)named-checkzone "straw.net" /var/named/straw.net.zone

- 配置主DNS服务器

  ![1548496239120](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1548496239120.png)

  ![1548496260821](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1548496260821.png)

  添加完RR后，还没结束，pa aux | grep named可以看出named进程的属主是named，而：

  ```shell
  [root@L named]# ll /var/named
  total 28
  drwxrwx---. 2 named named   49 Jan 13 17:27 data
  drwxrwx---. 2 named named   60 Jan  7 22:59 dynamic
  -rw-r--r--. 1 named named  720 Jan 26 17:27 managed-keys.bind
  -rw-r--r--. 1 named named  512 Jan 26 17:27 managed-keys.bind.jnl
  -rw-r-----. 1 root  named 2281 May 22  2017 named.ca
  -rw-r-----. 1 root  named  152 Dec 15  2009 named.empty
  -rw-r-----. 1 root  named  152 Jun 21  2007 named.localhost
  -rw-r-----. 1 root  named  168 Dec 15  2009 named.loopback
  drwxrwx---. 2 named named    6 Oct 31 08:29 slaves
  -rw-r--r--. 1 root  root   347 Jan 26 17:41 straw.net.zone
  ```

  区域文件权限不对，所以：

  ``` shell
  [root@L named]# chmod 640 straw.net.zone 
  [root@L named]# chown :named straw.net.zone 
  [root@L named]# ll
  total 28
  drwxrwx---. 2 named named   49 Jan 13 17:27 data
  drwxrwx---. 2 named named   60 Jan  7 22:59 dynamic
  -rw-r--r--. 1 named named  720 Jan 26 17:27 managed-keys.bind
  -rw-r--r--. 1 named named  512 Jan 26 17:27 managed-keys.bind.jnl
  -rw-r-----. 1 root  named 2281 May 22  2017 named.ca
  -rw-r-----. 1 root  named  152 Dec 15  2009 named.empty
  -rw-r-----. 1 root  named  152 Jun 21  2007 named.localhost
  -rw-r-----. 1 root  named  168 Dec 15  2009 named.loopback
  drwxrwx---. 2 named named    6 Oct 31 08:29 slaves
  -rw-r-----. 1 root  named  347 Jan 26 17:41 straw.net.zone
  [root@L named]# systemctl restart named
  ```

- 测试命令

  - dig

    dig [-t type] name [@SERVER] [query options]

  





## 日志系统rsyslog

历史日志：取舍、时间、时间

1. 日志级别Loglever——关不关键，要不要记录

2. 系统日志服务

   - syslog或rsyslog等系统日志服务能够让一些本身不想自我实现日志记录功能的程序，把日志信息发给rsyslog，实现日志记录。但是，很多较大并发访问的服务器软件，有可能自我实现日志系统，像httpd,ngnix,ssh等，它们可以选择支持这两种方式的其中一种日志记录格式。

   - syslog:

     (1)syslogd:system;

     (2)klogd:kernel

   - rsyslog:syslogd,klogd

     成为新一代的优势：

     (1)多线程；

     (2)TCP UDP SSL TLS 支持远程日志服务，开通远程机制，建立在某个套接字上，其他主机的所产生的日志信息，由本机的rsyslog收集起来，收集完后不负责记录，而是建立tcp或udp连接(明文，密文则是ssl或者tsl或者relp协议)，发给日志服务器。

     (3)支持MySQL, PGSQL, Oralce等关系型数据库，实现日志存储

     (4)强大的过滤器

     (5)可自定义输出格式

3. 日志收集分类——为N多应用程序收集日志，所以需要分类

   把某一类别的应用程序，归到一个类别中，通过一个统一管道，发送给rsyslog。

   将多个程序产生的日志流约束在同一个管道内，叫日志生成器——facility（设施）。

   - facility：auth, authpriv(认证和授权相关), cron, daemon,  kern, lpr(打印系统), mail, mark(标记相关), news, security, user, uucp(uucp协议), local0-local7(用户可以自定义使用的bander日志设施)

     facility是固定不变的，是rsyslog内置的

   - priority：debu(事无巨细，只要有信息就记录), info(信息级别，日志系统正常产生的信息), notice, warn(warning), err(error), crit(critical). alert, emerg(panic)

     指定级别：

     - *：所有级别
     - none:没有级别
     - priority:此级别以及更高级别的日志
     - =priority:此级别

   - facility.priority  /var/log/messages

4. 程序环境

   - 主程序：rsyslogd

   - 配置文件：/etc/rsyslog.conf  (这里不带d,是因为它既要为syslog记录日志，又要为klog记录日志，因此保留了早期不带d的配置文件格式 )

   - 服务脚本：/etc/rc.d/init.d/rsyslog  (centos6)  (syslog本身也可以监听在套接字上，向其他人提供服务，因此有服务脚本。它本身也会运行为服务)

   - rsyslog.conf  (修改之后需要restart服务而不是reload)

     ``` shell
     [root@L ~]# grep '####' /etc/rsyslog.conf
     #### MODULES ####
     #### GLOBAL DIRECTIVES ####
     #### RULES ####
     ```

     **RULES**:

      facility.priority  target

     ``` shell
     #### RULES ####
     
     # Log all kernel messages to the console.
     # Logging much else clutters up the screen.
     #kern.*                                                 /dev/console
     
     # Log anything (except mail) of level info or higher.
     # Don't log private authentication messages!
     *.info;mail.none;authpriv.none;cron.none                /var/log/messages
     
     # The authpriv file has restricted access.
     authpriv.*                                              /var/log/secure
     
     # Log all the mail messages in one place.
     mail.*                                                  -/var/log/maillog
     
     
     # Log cron stuff
     cron.*                                                  /var/log/cron
     
     # Everybody gets emergency messages
     *.emerg                                                 :omusrmsg:*
     
     # Save news errors of level crit and higher in a special file.
     uucp,news.crit                                          /var/log/spooler
     
     # Save boot messages also to boot.log
     local7.*                                                /var/log/boot.log 
     ```

     target:

     (1)文件路径，比如/var/log下某文件，文件路径前的“-”表示异步写入； [所以var目录被称为可变目录]

     (2)用户： *表示所有用户；

     (3)日志服务器： @host ,host必须要监听在tcp或udp协议514端口上提供服务；

     (4)管道：| COMMAD

     

     **日志格式**

     - 日期 主机名 进程(pid) : 事件内容

     - 有些日志是二进制格式：

       /var/log/wtmp：当前系统上成功登录的日志， last命令

       /var/log/btmp：当前系统上失败的登录尝试， lastb命令

       lastlog命令：显示当前系统每一个用户最近一次的登录时间

     

     

























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