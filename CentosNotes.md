



***

**不能即时消化的，就给我==详细记==！**

---



---

* [linux命令帮助获取详解](#linux%E5%91%BD%E4%BB%A4%E5%B8%AE%E5%8A%A9%E8%8E%B7%E5%8F%96%E8%AF%A6%E8%A7%A3)
  * [格式](#%E6%A0%BC%E5%BC%8F)
  * [内部命令](#%E5%86%85%E9%83%A8%E5%91%BD%E4%BB%A4)
  * [外部命令](#%E5%A4%96%E9%83%A8%E5%91%BD%E4%BB%A4)
    * [man手册](#man%E6%89%8B%E5%86%8C)
* [Linux的文件系统](#linux%E7%9A%84%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F)
  * [根文件系统(rootfs)](#%E6%A0%B9%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9Frootfs)
  * [应用程序的组成部分](#%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E7%9A%84%E7%BB%84%E6%88%90%E9%83%A8%E5%88%86)
* [BASH基础特性](#bash%E5%9F%BA%E7%A1%80%E7%89%B9%E6%80%A7)
  * [命令历史history](#%E5%91%BD%E4%BB%A4%E5%8E%86%E5%8F%B2history)
  * [命令hash](#%E5%91%BD%E4%BB%A4hash)
  * [命令和路径补全](#%E5%91%BD%E4%BB%A4%E5%92%8C%E8%B7%AF%E5%BE%84%E8%A1%A5%E5%85%A8)
  * [命令行展开](#%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%B1%95%E5%BC%80)
  * [命令的执行结果状态](#%E5%91%BD%E4%BB%A4%E7%9A%84%E6%89%A7%E8%A1%8C%E7%BB%93%E6%9E%9C%E7%8A%B6%E6%80%81)
  * [命令别名alias](#%E5%91%BD%E4%BB%A4%E5%88%AB%E5%90%8Dalias)
  * [文件名通配 globbing](#%E6%96%87%E4%BB%B6%E5%90%8D%E9%80%9A%E9%85%8D-globbing)
  * [快捷键](#%E5%BF%AB%E6%8D%B7%E9%94%AE)
  * [提供了编程环境](#%E6%8F%90%E4%BE%9B%E4%BA%86%E7%BC%96%E7%A8%8B%E7%8E%AF%E5%A2%83)
  * [bash的配置文件](#bash%E7%9A%84%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)
  * [bash的算术运算](#bash%E7%9A%84%E7%AE%97%E6%9C%AF%E8%BF%90%E7%AE%97)
  * [bash的条件测试](#bash%E7%9A%84%E6%9D%A1%E4%BB%B6%E6%B5%8B%E8%AF%95)
  * [bash自定义退出状态码](#bash%E8%87%AA%E5%AE%9A%E4%B9%89%E9%80%80%E5%87%BA%E7%8A%B6%E6%80%81%E7%A0%81)
* [CentOS启动流程](#centos%E5%90%AF%E5%8A%A8%E6%B5%81%E7%A8%8B)
  * [LinuxOS：kernel \+ rootfs](#linuxoskernel--rootfs)
  * [Linux内核特点](#linux%E5%86%85%E6%A0%B8%E7%89%B9%E7%82%B9)
  * [CenOS启动流程](#cenos%E5%90%AF%E5%8A%A8%E6%B5%81%E7%A8%8B)
  * [/sbin/init](#sbininit)
    * [CentOS 5](#centos-5)
    * [CentOS 6](#centos-6)
  * [Grub](#grub)
* [DNS and BIND](#dns-and-bind)
  * [DNS服务介绍](#dns%E6%9C%8D%E5%8A%A1%E4%BB%8B%E7%BB%8D)
  * [DNS服务器诞生由来](#dns%E6%9C%8D%E5%8A%A1%E5%99%A8%E8%AF%9E%E7%94%9F%E7%94%B1%E6%9D%A5)
  * [区域解析库](#%E5%8C%BA%E5%9F%9F%E8%A7%A3%E6%9E%90%E5%BA%93)
    * [RR类型：](#rr%E7%B1%BB%E5%9E%8B)
    * [RR格式](#rr%E6%A0%BC%E5%BC%8F)
  * [子域授权](#%E5%AD%90%E5%9F%9F%E6%8E%88%E6%9D%83)
  * [BIND的安装配置](#bind%E7%9A%84%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE)
* [日志系统rsyslog](#%E6%97%A5%E5%BF%97%E7%B3%BB%E7%BB%9Frsyslog)
* [文本处理三剑客](#%E6%96%87%E6%9C%AC%E5%A4%84%E7%90%86%E4%B8%89%E5%89%91%E5%AE%A2)
  * [grep](#grep)
* [进程管理工具](#%E8%BF%9B%E7%A8%8B%E7%AE%A1%E7%90%86%E5%B7%A5%E5%85%B7)
* [计划任务](#%E8%AE%A1%E5%88%92%E4%BB%BB%E5%8A%A1)
  * [at](#at)
  * [batch](#batch)
  * [cron](#cron)

---




















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



### 命令和路径补全





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





## CentOS启动流程



### LinuxOS：kernel + rootfs

每时每刻，OS要么执行内核代码，要么执行rootfs某个路径下的应用代码

- kernel: 进程管理、内存管理、网络管理、驱动程序、文件系统、安全功能(selinux,权限功能)、
- rootfs: 
  (1)把系统调用封装在二进制界面，叫做glibc；
  (2)根文件系统上最重要的是二进制程序文件。
  - 库：函数集合,其实是功能模块 function,
    任何功能有其调用接口，调用接口的名字称为函数名。
    为了函数永远更灵活的功能，函数还能接受参数;
    每一个库中有多少个函数，每一个函数能够接受多少参数，每一个参数是什么类型，都有一个文件加以描述，这个文件叫做头文件。
    库也是二进制程序，但跟bin下应用程序二进制文件不同，库没有独立执行入口，只能被调用。
    库有两种情形：调用完后有返回值(状态结果)，无返回值；无返回值的代码片段叫做过程调用，有返回值的叫函数调用。
  - 程序
    库或者内核本身都不能产生结果，需要在组织上一块运行才能产生结果，这就是应用程序。保证程序按照我们的需求运行才是根本。(配置文件)
- 简要启动过程：
  内核运行后，加载根文件系统，因为内核无论怎么运行，都不能满足用户的实际需要，所以内核要想办法去运行应用程序；
  应用程序有千千万，所以内核委派一个使者(init)去管理。

### Linux内核特点

单内核设计(把所有功能集成于同一个程序)，支持模块化(内核模块.ko;用户模块.so)

``` shell
[root@pirate ~]# ls /boot/  
config-2.6.32-696.el6.x86_64         lost+found
efi                                  symvers-2.6.32-696.el6.x86_64.gz
grub                                 System.map-2.6.32-696.el6.x86_64
initramfs-2.6.32-696.el6.x86_64.img  vmlinuz-2.6.32-696.el6.x86_64
[root@pirate ~]# ls -lh /boot/vmlinuz-2.6.32-696.el6.x86_64
-rwxr-xr-x. 1 root root 4.1M 3月  22 2017 /boot/vmlinuz-2.6.32-696.el6.x86_64
[root@pirate ~]# file /boot/vmlinuz-2.6.32-696.el6.x86_64
/boot/vmlinuz-2.6.32-696.el6.x86_64: Linux kernel x86 boot executable bzImage, version 2.6.32-696.el6.x86_64 (mockbuil, RO-rootFS, swap_dev 0x4, Normal VGA
[root@pirate ~]# ls /lib/modules/2.6.32-696.el6.x86_64/
build              modules.dep          modules.networking  modules.symbols.bin
extra              modules.dep.bin      modules.ofmap       modules.usbmap
kernel             modules.drm          modules.order       source
modules.alias      modules.ieee1394map  modules.pcimap      updates
modules.alias.bin  modules.inputmap     modules.seriomap    vdso
modules.block      modules.isapnpmap    modules.softdep     weak-updates
modules.ccwmap     modules.modesetting  modules.symbols
[root@pirate ~]# ls /lib/modules/2.6.32-696.el6.x86_64/kernel/
arch  crypto  drivers  fs  kernel  lib  mm  net  sound
[root@pirate ~]# du -sh /lib/modules/2.6.32-696.el6.x86_64/
114M    /lib/modules/2.6.32-696.el6.x86_64/
```

- 组成部分：
  1. 核心文件：/boot/vmlinuz-VERSION-release
  2. ramdisk：非必要组件，但在很多场景中会用到；为内核提供(硬盘)驱动
     CentOS 5: /boot/initrd-VERSION-release.img
     CentOS 6: /boot/initramfs-VERSION-release.img
  3. 模块文件：/lib/modules/VERSION-release

### CenOS启动流程

加电自检--> BootSequence (BIOS) --> Bootloader(MBR) --> kernel(ramdisk) --> rootfs(只读) --> init

> 	init程序的类型：
> 		SysV: init, CentOS 5  配置文件：/etc/inittab
> 		Upstart: init, CentOS 6  配置文件：/etc/inittab, /etc/init/*.conf
> 		Systemd：systemd, CentOS 7  配置文件：/usr/lib/systemd/system, /etc/systemd/system
> 		
>
> 		ramdisk：
> 		内核中的特性之一：使用缓冲和缓存来回事对磁盘上的文件访问；
> 		
> 		ramdisk --> ramfs
> 		CentOS 5: initrd,  工具程序：mkinitrd
> 		CentOS 6: initramfs， 工具程序：mkinitrd, dracut

后续工作都交给init，init怎么做完全取决于其配置文件的定义。



### /sbin/init

#### CentOS 5

- 运行级别：类似安全模式，为了系统的运行或维护等应用目的而设定

  > 0-6：7个级别
  > 0：关机
  > 1：单用户模式(root, 无须登录), single, 维护模式；
  > 2:   多用户模式，会启动网络功能，但不会启动NFS；维护模式；
  > 3：多用户模式，正常模式；文本界面；
  > 4：预留级别；可同3级别；
  > 5：多用户模式，正常模式；图形界面；
  > 6：重启

  切换级别：init #
  查看上一级别与当前级别：runlevel和who -r

- **配置文件**：/etc/inittab

  id:runlevel:action:process
  每一行定义一种action以及与之对应的process

  1. 各级别启动的服务
  
     si::sysinit:/etc/rc.d/rc.sysinit
  
     l0:0:wait:/etc/rc.d/rc 0
     l1:1:wait:/etc/rc.d/rc 1
     ...
     l6:6:wait:/etc/rc.d/rc 6
     
     - 说明：rc 0 --> 意味着读取/etc/rc.d/rc0.d/
       K*: K##*：##运行次序；数字越小，越先运行；数字越小的服务，通常为依赖到别的服务；
       S*: S##*：##运行次序；数字越小，越先运行；数字越小的服务，通常为被依赖到的服务；
     
     - ``` 
       [root@localhost ~]# ls /etc/rc.d/
       init.d/     rc0.d/      rc2.d/      rc4.d/      rc6.d/      rc.sysinit
       rc          rc1.d/      rc3.d/      rc5.d/      rc.local
       ```
     
       init.d下是开机脚本，rc0-6是六个级别下链接到init.d的一些K#或S#软链接。
       要知道哪个脚本在哪个级别下是启动还是关闭的，可以用chkconfig命令。
     
       **chekconfig**
     
       1. 查看  chkconfig --list [name]
     
       2. 添加  chkconfig --add name
     
          ```
          [root@localhost ~]# cat /etc/rc.d/init.d/testsrv2
          #!/bin/bash
          #chkconfig: 3456 44 22
          #description: test srv
          echo "srv test"
          [root@localhost ~]# chmod +x /etc/rc.d/init.d/testsrv2
          [root@localhost ~]# ll /etc/rc.d/init.d/testsrv2
          -rwxr-xr-x 1 root root 74 2018-04-08 /etc/rc.d/init.d/testsrv2
          [root@localhost ~]# chkconfig --add testsrv2
          [root@localhost ~]# chkconfig --list testsrv2
          testsrv2        0:关闭  1:关闭  2:关闭  3:启用  4:启用  5:启用  6:启用
          [root@localhost ~]# ll /etc/rc.d/rc6.d/S44testsrv2 
          lrwxrwxrwx 1 root root 18 2018-04-08 /etc/rc.d/rc6.d/S44testsrv2 -> ../init.d/testsrv2
          [root@localhost ~]# ll /etc/rc.d/rc0.d/K22testsrv2 
          lrwxrwxrwx 1 root root 18 2018-04-08 /etc/rc.d/rc0.d/K22testsrv2 -> ../init.d/testsrv2
          ```
     
          开机脚本的注释内容里，3456级别默认开启testsrv2脚本，没提到的012级别默认关闭，优先级为S44或K22
     
       3. 删除  chkconfig --del name
     
       4. 修改  chkconfig [--level levels] name <on|off|reset>
          --level省略时表示2345级别
     
       5. 注意：正常级别下，最后启动一个服务S99local没有链接至/etc/rc.d/init.d一个服务脚本，而是指向了/etc/rc.d/rc.local脚本；因此，不便或不需写为服务脚本放置于/etc/rc.d/init.d/目录，且又想开机时自动运行的命令，可直接放置于/etc/rc.d/rc.local文件中。
     
  2. 启动终端设备，关联登录程序
  
     1:2345:respawn:/sbin/mingetty tty1
     2:2345:respawn:/sbin/mingetty tty2
     3:2345:respawn:/sbin/mingetty tty3
     4:2345:respawn:/sbin/mingetty tty4
     5:2345:respawn:/sbin/mingetty tty5
     6:2345:respawn:/sbin/mingetty tty6
  
     表示启动6个虚拟终端;在2345级别下启动;用户在终端Logout后，这个终端不会没，而会立即在重启一个终端给用户登录，这就是respawn;Mingetty会自动调用login程序,login程序显示登录提示符给你，给你验证账号密码正确后，给你启动默认shell进程。
     
  3. 系统初始化脚本：/etc/rc.d/rc.sysinit
  
     (1) 设置主机名；
     (2) 设置欢迎信息；
     (3) 激活udev和selinux;
     (4) 挂载/etc/fstab文件中定义的文件系统；
     (5) 检测根文件系统，并以读写方式重新挂载根文件系统；
     (6) 设置系统时钟；
     (7) 激活swap设备；
     (8) 根据/etc/sysctl.conf文件设置内核参数；
     (9) 激活lvm及software raid设备；
     (10) 加载额外设备的驱动程序；
     (11) 清理操作；
     
     ==rc.sysinit脚本要细看，看懂，可用于学shell编程==
  
- 总结：
  
  /sbin/init --> (/etc/inittab) --> 设置默认运行级别 --> 运行系统初始脚本、完成系统初始化 --> 关闭对应下需要关闭的服务，启动需要启动服务 --> 设置登录终端
  
  
#### CentOS 6

init程序是upstart，但依然命名为init，其配置文件：
/etc/inittab，os6inittab文件下只有这一行`id:5:initdefault:`，这个文件是centos在组织时为了方便用户改默认级别而有意设定的，其实6的配置文件主要是/etc/init/*.conf

``` 
[root@pirate init.d]# cd /etc/init
[root@pirate init]# ls
ck-log-system-restart.conf  rcS.conf
ck-log-system-start.conf    rcS-emergency.conf
ck-log-system-stop.conf     rcS-sulogin.conf
control-alt-delete.conf     readahead-collector.conf
init-system-dbus.conf       readahead.conf
kexec-disable.conf          readahead-disable-services.conf
plymouth-shutdown.conf      serial.conf
prefdm.conf                 splash-manager.conf
quit-plymouth.conf          start-ttys.conf
rc.conf                     tty.conf
[root@pirate init]# cat rc.conf
# rc - System V runlevel compatibility
#
# This task runs the old sysv-rc runlevel scripts.  It
# is usually started by the telinit compatibility wrapper.
#
# Do not edit this file directly. If you want to change the behaviour,
# please create a file rc.override and put your changes there.

start on runlevel [0123456]

stop on runlevel [!$RUNLEVEL]

task

export RUNLEVEL
console output
exec /etc/rc.d/rc $RUNLEVEL
```

rc.conf是启动服务的，rcS.conf是启动脚本的。
不用专门学习upstart语法，因为7版本大变化，而且大多数时候是改服务脚本:/etc/rc.d/init.d/*

-  CentOS 6启动流程：
    		POST --> Boot Sequence(BIOS) --> Boot Loader (MBR) --> Kernel(ramdisk) --> rootfs --> switchroot --> /sbin/init -->(/etc/inittab, /etc/init/*.conf) --> 设定默认运行级别 --> 系统初始化脚本 --> 关闭或启动对应级别下的服务 --> 启动终端

  

  ### Grub

grub: GRand Unified Bootloader

grub 0.x: grub legacy

grub 1.x: grub2  完全重写的版本，只是在某些特性上再兼容gurb legacy

1. grub legacy

   stage1: 安装在mbr中
   stage1_5: mbr之后的扇区，给grub提供文件系统驱动，让stage1中的bootloader能识别stage2所在的分区上的文件系统；
   stage2：磁盘分区(/boot/grub/)，此磁盘分区上不单有第二阶段，还有内核文件以及ramdisk等等，此阶段是那个可编辑的grub界面

   配置文件：/boot/grub/grub.conf <-- /etc/grub.conf

2. grub的命令行接口

   **grub的作用无非就是加载用户所选定的内核，关键是内核存在于哪个磁盘哪个分区**。

   help: 获取帮助列表
   help KEYWORD: 详细帮助信息
   find (hd#,#)/PATH/TO/SOMEFILE：
   root (hd#,#)  不是指根文件系统所在的设备，而是grub第二阶段所在的磁盘分区
   kernel /PATH/TO/KERNEL_FILE: 设定本次启动时用到的内核文件；额外还可以添加许多内核支持使用的cmdline参数；
   例如：init=/path/to/init, selinux=0
   initrd /PATH/TO/INITRAMFS_FILE: 设定为选定的内核提供额外文件的ramdisk；ramdisk必须与内核版本号完全匹配。
   boot: 引导启动选定的内核；
   
   > 手动在grub命令行接口启动系统：
   > 				grub> root (hd#,#)
   > 				grub> kernel /vmlinuz-VERSION-RELEASE ro root=/dev/DEVICE 
   > 				grub> initrd /initramfs-VERSION-RELEASE.img
   > 				grub> boot
   
3. 配置文件：/boot/grub/grub.conf

   手动用命令行接口启动系统比较麻烦，所以有配置文件事先配好那个grub启动页面。

   ``` shell
   # Note that you do not have to rerun grub after making changes to this file
   # NOTICE:  You have a /boot partition.  This means that
   #          all kernel and initrd paths are relative to /boot/, eg.
   #          root (hd0,0)
   #          kernel /vmlinuz-version ro root=/dev/sda2
   #          initrd /initrd-[generic-]version.img
   #boot=/dev/sda1
   
   #password选项可以用openssl命令，但用grub-md5-crypt命令更方便。
   default=0
   timeout=5
   splashimage=(hd0,0)/grub/hubble.xpm.gz
   password --md5 $1$3rS1B0$UQlc0ljZr2bNT5Qajj0Ev1
   hiddenmenu
   title CentOS 6 (2.6.32-696.el6.x86_64)
           root (hd0,0) #0表示第1块硬盘
           kernel /vmlinuz-2.6.32-696.el6.x86_64 ro root=UUID=f8936b5e-5671-4f57-a704
   -cd5e7a815e1b rd_NO_LUKS  KEYBOARDTYPE=pc KEYTABLE=us rd_NO_MD crashkernel=auto LA
   NG=zh_CN.UTF-8 rd_NO_LVM rd_NO_DM rhgb quiet
           initrd /initramfs-2.6.32-696.el6.x86_64.img
   #second grub
   title grubLearning-CentOs6 (2.6.32-696.el6.x86_64)
           root (hd0,0)
           kernel /vmlinuz-2.6.32-696.el6.x86_64 ro root=UUID=f8936b5e-5671-4f57-a704
   -cd5e7a815e1b rd_NO_LUKS  KEYBOARDTYPE=pc KEYTABLE=us rd_NO_MD crashkernel=auto LA
   NG=zh_CN.UTF-8 rd_NO_LVM rd_NO_DM rhgb quiet
           initrd /initramfs-2.6.32-696.el6.x86_64.img
           password --md5 $1$3rS1B0$UQlc0ljZr2bNT5Qajj0Ev1
   ```

4. 进入单用户模式

   (1) 编辑grub菜单(选定要编辑的title，而后使用e命令);
   (2) 在选定的kernel后附加1, s, S或single都可以；
   (3) 在kernel所在行，键入“b”命令；
   
5. 安装grub

   场景1：双系统下重装win10，grub被覆盖，将硬盘拆下来装到其他主机上，给这个硬盘新装个grub。

   （1）在正常主机上的/mnt/boot目录挂载没有grub的那个硬盘sdc；

   （2）给其安装grub，指定根目录是/mnt，grub-install会自己找寻boot目录；(如果sdc没有内核文件，也一并复制给它)

   （3）配置grub.conf

   （4）系统要跑起来，还需要根文件系统和bash

   （5）额外加一项给grub.conf,限定init是/bin/bash而不是/sbin/init

   ``` shell
   #(1)
   [root@pirate ~]# mkdir /mnt/boot
   [root@pirate ~]# mount /dev/sdc1 /mnt/boot
   [root@pirate ~]# ls /mnt/boot
   lost+found
   #(2)
   [root@pirate ~]# grub-install --root-directory=/mnt /dev/sdc
   Probing devices to guess BIOS drives. This may take a long time.
   Unknown partition table signature
   Unknown partition table signature
   Unknown partition table signature
   Unknown partition table signature
   Unknown partition table signature
   Unknown partition table signature
   Unknown partition table signature
   Unknown partition table signature
   Unknown partition table signature
   Unknown partition table signature
   Unknown partition table signature
   Unknown partition table signature
   Unknown partition table signature
   Unknown partition table signature
   Installation finished. No error reported.
   This is the contents of the device map /mnt/boot/grub/device.map.
   Check if this is correct or not. If any of the lines is incorrect,
   fix it and re-run the script `grub-install'.
   
   (fd0)   /dev/fd0
   (hd0)   /dev/sda
   (hd1)   /dev/sdb
   (hd2)   /dev/sdc
   [root@pirate ~]# ls /mnt/boot
   grub  lost+found
   [root@pirate ~]# ls /mnt/boot/grub
   device.map     ffs_stage1_5      minix_stage1_5     stage2           xfs_stage1_5
   e2fs_stage1_5  iso9660_stage1_5  reiserfs_stage1_5  ufs2_stage1_5
   fat_stage1_5   jfs_stage1_5      stage1             vstafs_stage1_5
   [root@pirate ~]# cp /boot/vmlinuz-2.6.32-696.el6.x86_64 /mnt/boot/vmlinuz
   [root@pirate ~]# cp /boot/initramfs-2.6.32-696.el6.x86_64.img /mnt/boot/initramfs.img
   #(3)
   [root@pirate ~]# vim /mnt/boot/grub/grub.conf
   default=0
   timeout=5
   title grub-instll-Learning Centos6
           root (hd0,0) #这块硬盘装会原主机，是原主机的第一块硬盘
           kernel /vmlinuz ro root=/dev/sda2 #这里的root是指真正根文件系统的根，sdc2装回原主机是变成sda2
           initrd /initramfs.img
   #(4)
   [root@pirate ~]# mkdir /mnt/sysroot
   [root@pirate ~]# mount /dev/sdc2 /mnt/sysroot
   [root@pirate ~]# cd /mnt/sysroot
   [root@pirate sysroot]# mkdir -pv etc bin sbin lib lib64 dev proc sys tap var usr home root mnt media
   mkdir: 已创建目录 "etc"
   mkdir: 已创建目录 "bin"
   mkdir: 已创建目录 "sbin"
   mkdir: 已创建目录 "lib"
   mkdir: 已创建目录 "lib64"
   mkdir: 已创建目录 "dev"
   mkdir: 已创建目录 "proc"
   mkdir: 已创建目录 "sys"
   mkdir: 已创建目录 "tap"
   mkdir: 已创建目录 "var"
   mkdir: 已创建目录 "usr"
   mkdir: 已创建目录 "home"
   mkdir: 已创建目录 "root"
   mkdir: 已创建目录 "mnt"
   mkdir: 已创建目录 "media"
   [root@pirate sysroot]# ldd /bin/bash  #查询bash程序需要哪些库文件，然后相应复制给sdc2
           linux-vdso.so.1 =>  (0x00007ffe7eb25000) #第一个.so只是库文件的访问入口
           libtinfo.so.5 => /lib64/libtinfo.so.5 (0x00000033d5000000)
           libdl.so.2 => /lib64/libdl.so.2 (0x00000033cd000000)
           libc.so.6 => /lib64/libc.so.6 (0x00000033cd400000)
           /lib64/ld-linux-x86-64.so.2 (0x00000033ccc00000)
   [root@pirate sysroot]# cp /lib64/libtinfo.so.5 /mnt/sysroot/lib64/
   [root@pirate sysroot]# cp /lib64/libdl.so.2 /mnt/sysroot/lib64/
   [root@pirate sysroot]# cp /lib64/libc.so.6 /mnt/sysroot/lib64/ 
   [root@pirate sysroot]# cp /lib64/ld-linux-x86-64.so.2 /mnt/sysroot/lib64/
   [root@pirate ~]# chroot /mnt/sysroot/ #测试能否使用bash
   bash-4.1# 
   bash-4.1# ls
   bash: ls: command not found
   bash-4.1# exit
   exit
   #(5)
   [root@pirate ~]# vim /mnt/boot/grub/grub.conf
   default=0
   timeout=5
   title grub-instll-Learning Centos6
           root (hd0,0)
           kernel /vmlinuz ro root=/dev/sda2 init=/bin/bash
           initrd /initramfs.img
   [root@pirate ~]# sync
   ```

   场景2：本机的grub被自己敲坏了，但还没重启。
   
   （1）手动吧本机磁盘mbr上的bootloader敲坏，只破坏前446个字节而不破坏分区表；
   
   （2）第一种修复方法：grub-intall命令安装；[并不要求指定的根下有boot目录、grub目录及文件]
   
   （3）第二种：敲grub进入grub界面，然后setup安装。[要求hd#上有grub目录，里面stage1,1,5,2都得存在]
   
   ``` shell
   #(1)备份，写入
   [root@pirate ~]# dd if=/dev/sda of=/root/mbr.bak count=1 bs=512
   记录了1+0 的读入
   记录了1+0 的写出
   512字节(512 B)已复制，0.333071 秒，1.5 kB/秒
   [root@pirate ~]# dd if=/dev/zero of=/dev/sda bs=200 count=1
   记录了1+0 的读入
   记录了1+0 的写出
   200字节(200 B)已复制，0.000385927 秒，518 kB/秒
   #(2)
   [root@pirate ~]# grub-install --root-directory=/ /dev/sda
   Installation finished. No error reported.
   This is the contents of the device map //boot/grub/device.map.
   Check if this is correct or not. If any of the lines is incorrect,
   fix it and re-run the script `grub-install'.
   
   # this device map was generated by anaconda
   (hd0)     /dev/sda
   [root@pirate ~]# 
   #(3)再破坏，然后进入grub界面setup
   [root@pirate ~]# dd if=/dev/zero of=/dev/sda bs=200 count=1
   记录了1+0 的读入
   记录了1+0 的写出
   200字节(200 B)已复制，0.000324817 秒，616 kB/秒
   [root@pirate ~]# grub
   Probing devices to guess BIOS drives. This may take a long time.
   Unknown partition table signature
   
   
       GNU GRUB  version 0.97  (640K lower / 3072K upper memory)
   
    [ Minimal BASH-like line editing is supported.  For the first word, TAB
      lists possible command completions.  Anywhere else TAB lists the possible
      completions of a device/filename.]
   grub> root (hd0,0)
   root (hd0,0)
    Filesystem type is ext2fs, partition type 0x83
   grub> setup (hd0)
   setup (hd0)
    Checking if "/boot/grub/stage1" exists... no
    Checking if "/grub/stage1" exists... yes
    Checking if "/grub/stage2" exists... yes
    Checking if "/grub/e2fs_stage1_5" exists... yes
    Running "embed /grub/e2fs_stage1_5 (hd0)"...  27 sectors are embedded.
   succeeded
    Running "install /grub/stage1 (hd0) (hd0)1+27 p (hd0,0)/grub/stage2 /grub/grub.conf"... succeeded
   Done.
   grub> quit
   quit
   [root@pirate ~]# sync
   ```
   
   ![grub1](https://raw.githubusercontent.com/strawleave/PicBase/master/内核启动了selinux而boot时找不到selinux策略.jpg)
   
   ![grub1](https://raw.githubusercontent.com/strawleave/PicBase/master/Grub界面手动启动内核.jpg)

  

  

  

  

































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

  - 出现的内容：(1)宏定义[比如开头的$TTL 86400]；(2)资源记录

  - 主要由资源记录组成，编辑完之后检查：

    (1)named-checkconf

    (2)named-checkzone "straw.net" /var/named/straw.net.zone

- 配置主DNS服务器

  ![1548496239120](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1548496239120.png)

  ![1548496260821](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1548496260821.png)

  添加完RR后，还没结束，ps aux | grep named可以看出named进程的属主是named，而/var/named下的文件属主都是root,属组都是named，但自己创建的zone文件则权限是root:root，这会导致named用户无权限访问straw.net.zone：

  ```shell
  [root@L named]# ps aux | grep named
  named     22196  0.0  1.5 240224 15348 ?        Ssl  07:59   0:00 /usr/sbin/named -u named -c /etc/named.conf
  root      22272  0.0  0.0 112676   976 pts/0    S+   08:26   0:00 grep --color=auto named
  [root@L ~]# ll /etc/named.conf  #主配置文件表明name最基本的权限形式root:named
  -rw-r-----. 1 root named 1830 7月  16 08:05 /etc/named.conf
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
dig用于测试dns系统，因此，不会查询hosts文件进行解析；
    dig [-t type] name [@SERVER] [query options]
  dig时如果不带@某主机，则默认是向/etc/resolve.conf里写的namesever去请求解析。
  
  





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

1. pstree

2. ps:report a snapshot of the current processes. 报告静态信息
   伪文件系统proc，只是被内核映射成目录和文件而已
   ![proc](https://raw.githubusercontent.com/strawleave/PicBase/master/proc伪文件系统.png)

   每一个目录名代表进程号，每一个目录里面的文件代表一个进程相关的状态信息。
   每个目录下的cmdline文件内容代表该进程是由哪一个命令启动的。
   
3. pgrep,pkill
   pgrep -u root -l
   pgrep sshd

4. top,htop

5. vmstat

6. pmap
   报告进程从线性地址到物理地址的映射关系
   pmap pid

7. dstat
   dstat -C 0,1,total -D total,sda
   dstat -l  动态显示过去1分钟、5分钟、15分钟的平均负载
   dstat -m  内存显示
   dstat -n  网络收发显示
   dstat --tcp   --udp   --raw    --unix   --socket
   dstat --ipc  显示进程间通信
   dstat --top-cpu   --top-io   --top-mem   --top-latency 显示延迟最大的进程

8. kill
   向进程发送控制信号，以实现对进程管理
   显示可发送的信号：kill -l  或  man 7 signal

   - 常用信号：
     1) SIGHUP: 无须关闭进程而让其重读配置文件；(对服务端管理进程很重要)
     2) SIGINT: 中止正在运行的进程；相当于Ctrl+c；
     9) SIGKILL: 杀死正在运行的进程；(直接杀)
     15) SIGTERM：终止正在运行的进程；(人道处死)
     18) SIGCONT：让其继续运行
     19) SIGSTOP：让其处于停止态
   - 指定信号的方法：
     (1) 信号的数字标识；1, 2, 9
     (2) 信号完整名称；SIGHUP
     (3) 信号的简写名称；HUP
   - 向进程发信号：
     kill [-SIGNAL] PID...
   - 终止“名称”之下的所有进程：
     killall [-SIGNAL] Program
     比如httpd无论何时都保持至少5个进程，杀一个起一个，可以用killall -15 httpd

9. Linux的作业控制jobs

   - 前台作业：通过终端启动，且启动后一直占据终端；(比如top)
     后台作业：可以通过终端启动，但启动后即转入后台运行（释放终端）；

   - 如何让作业运行于后台？
     (1) 运行中的作业
     Ctrl+z  (fg命令调回)
     (2) 尚未启动的作业
     COMMAD &  (让其在启动之后立即转为后台)

     注：此类作业虽然被送往后台运行，但其依然与终端相关；如果希望送往后台后，剥离与终端的关系：nohup COMMAD &
     
   - 查看被ctrl+z的所有作业,用jobs命令
   
- 作业控制
   fg [[%]JOB_NUM]：把指定的后台作业调回前台；
     bg [[%]JOB_NUM]：让送往后台的作业在后台继续运行；
   kill [%JOB_NUM]：终止指定的作业；(%不能省略，不然会被当成PID)
   
     与终端无关的job，使用ctrl+c是没法停止的，其信号捕获不到。
     ctrl+c信号只能通过终端捕获后送给进程
   
10.      进程优先级调整
         用户空间可以通过调整进程的Nice值来改变它的优先级。
         手动修改是静态优先级，100-139，
         nice值范围是-20-19，
         如果内核发现某个进程占用过多cpu，会自动惩罚降低其优先级，
         进程默认启动时的nice值为0，优先级为120;
         优先级数字越小，优先级越高。
         nice -n 5 htop
         ps axo pid,comm,nice
         renice -n  2 PID
         普通用户只能调高nice值，即调低优先级；管理员可随意调整。



## 计划任务

未来的某时间点执行一次任务：at, batch
周期性运行某任务: cron



### at

```
[root@pirate ~]# at 09:28
at> ls /var
at> cat /etc/fstab
at> <EOT>
job 1 at 2018-12-26 09:28
```

at某一时间点后，写完命令，ctrl+d提交，到时的结果会以邮件形式传送。

- 电子邮件服务：
  smtp: simple mail transmission protocol, 只能用于传送邮件；
  pop3: Post Office Protocol, 邮筒；
  imap4：Internet Mail Access Protocol, 邮筒，更强大复杂些。

- Linux主机自行内部有很多维护工作，维护结果需要通知给相关账户。
  使用ss -tnl就知道，默认有监听127.0.0.1:25，说明该smtp协议不准备与外界联系，只用于本地一个账号发给另一个账号。这里连"邮筒"都用不上，用的是/var/spool/mail的目录，mailbox模式。
  邮件放置方式有两种：mailbox(邮件数据流在一个文件里存放)和mailderectory(每一封邮件都是用单独的文件在一个目录下存放)

- 帮用户收发邮件的服务：
  mailx - send and receive Internet mail
  MUA：Mail User Agent

  ```shell
  #发给自己
  [root@pirate ~]# mailx -s "hello" root@localhost
  pirate
  qianli
  jinji
  EOT
  [root@pirate ~]# mail
  Heirloom Mail version 12.4 7/29/08.  Type ? for help.
  "/var/spool/mail/root": 2 messages 1 new
      1 root                  Wed Dec 26 09:28  50/1393  "Output from your job   "
  >N  2 root                  Wed Dec 26 10:05  21/612   "hello"
  & 2
  
  #发给其他用户                               
  [root@pirate ~]# mailx -s "he" yao@localhost < mail.txt
  [root@pirate ~]# su - yao
  [yao@pirate ~]$ mail
  Heirloom Mail version 12.4 7/29/08.  Type ? for help.
  "/var/spool/mail/yao": 1 message 1 new
  >N  1 root                  Wed Dec 26 10:09  18/613   "he"
  & 
  ```

  > mailx [-s 'SUBJECT'] username[@hostname]
  > 邮件正文的生成：
  > (1) 直接给出，Ctrl+d;
  > (2) 输入重定向；
  > (3) 通过管道；
  > 	echo -e "How are you?\nHow old are you?" | mail

- 注意环境变量，给命令时建议用绝对路径，或脚本里自己定义PATH

- 常用选项
  -q QUEUE: 有队列a,b,c...
  -l: 列出指定队列中等待运行的作业；相当于atq
  -d: 删除指定的作业；相当于atrm
  -c: 查看具体作业任务；
  -f /path/from/somefile：从指定的文件中读取任务；

  ``` 
  [root@pirate ~]# at now+2minutes
  at> cat /etc/issue
  at> echo "hzw:^H"
  at> <EOT>
  job 2 at 2018-12-26 10:27
  [root@pirate ~]# at -l
  2       2018-12-26 10:27 a root
  [root@pirate ~]# atq
  2       2018-12-26 10:27 a root
  [root@pirate ~]# at -d 2
  [root@pirate ~]# at -l
  
  [root@pirate ~]# at -f at.task now+10minutes
  job 4 at 2018-12-26 10:44
  ```



### batch

让系统自行选择空闲时间去执行此处指定的任务



### cron

- ``` 
  [root@pirate ~]# rpm -qa | grep cron
  cronie-anacron-1.4.4-16.el6_8.2.x86_64
  cronie-1.4.4-16.el6_8.2.x86_64
  crontabs-1.10-33.el6.noarch
  ```

  相关程序包
  cronie: 主程序包，提供了crond守护进程及相关辅助工具；
  cronie-anacron：cronie的补充程序；用于监控cronie任务执行状况；如cronie中的任务在过去该运行的时间点未能正常运行，则anacron会随后启动一次此任务；
  crontabs：包含CentOS提供系统维护任务,这些任务在cronnie或**crond中运行**，所以应确保crond守护处于运行状态。

  

- 计划要周期性执行的任务提交给crond，由其来实现到点运行。系统cron任务：
  系统维护作业:：/etc/crontab
  用户cron任务：crontab命令
  
- Example of job definition:

  ``` 
  .---------------- minute (0 - 59)
  |  .------------- hour (0 - 23)
  |  |  .---------- day of month (1 - 31)
  |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
  |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR 
  |  |  |  |  |
  *  *  *  *  * user-name  command to be executed
  ```

- 时间表示法：
  (1) 特定值；
  给定时间点有效取值范围内的值；
  例如：晚上9点10分运行echo命令；
  10 21 * * *	 gentoo /bin/echo "Howdy!"

  (2) *
  给定时间点上有效取值范围内的所有值；
  表示“每...”；

  (3) 离散取值：,
  #,#,#
  (4) 连续取值：-
  #-#
  (5) 在指定时间范围上，定义步长：
  /#: #即为步长
  例1：每3分钟： */3 * * * *

  例2：* */3 * * * 每3小时到了，那一小时内每分钟都执行一次，因为分钟那里是*；

  0 */3 * * *  这个每3小时执行一次，因为分钟那里是一个特定时间点。

- 用户cron
  crontab命令定义，每个用户都有专用的cron任务文件：/var/spool/cron/USERNAME

  注意：运行结果以邮件通知给相关用户；
  (1) COMMAND > /dev/null
  (2) COMMAND &> /dev/null

  对于cron任务来讲，%有特殊用途；如果在命令中要使用%，则需要转义；不过，如果把%放置于单引号中，也可以不用转义；

  

  

