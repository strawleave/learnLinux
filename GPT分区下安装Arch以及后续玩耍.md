[TOC]







### 序

- 个人经验记录190217，参考https://www.viseator.com/2017/05/17/arch_install/
- 本机联想Y485P, A10, A卡双显卡

















### 制作U盘启动盘

1. 到<https://www.archlinux.org/download/>页面下方的中国镜像源中下载`archlinux-**-x86_64.iso`这个`iso`文件。

2. win: fedoramediawriter-win32-4.0.7.exe

   Linux:dd命令，http://www.runoob.com/linux/linux-comm-dd.html （未尝试）



### 安装

#### 从U盘启动

进BIOS设置启动顺序或者直接按F12选择从U盘进入；
显示的Arch启动页面选第一选项；
__注意：__Waiting 30 seconds for device /dev/disk/by-label/ARCH_201811时，拔插一下U盘，就能顺利进入了。



#### 检查引导方式

ls /sys/firmware/efi/efivars 能正常显示路径说明是EFI引导+GPT分区表



#### 联网

- ping www.baidu.com
- dhcpcd
- wifi-menu

#### 更新系统时间

timedatectl set-ntp true



#### 分区与格式化

1. 查看分区状态：fdisk -l
2. 引导分区：fdisk /dev/sda  g(创建全新的gpt分区表，已有分区表的则直接创建根目录)  n  +512M  t(调整分区类型)  ef(更改分区类型为EFI)  w  mkfs.fat -F32 /dev/sda1
3. 根目录：fdisk /dev/sda  n  +5G  w  mkfs.ext4 /dev/sda2



#### 挂载分区

现在是在U盘的Linux Live安装盘, 仅仅有一些Linux基础目录结构，无多少数据，比如/mnt目录就是空的，接下来要将刚才创建的根分区/dev/sda2(这是设备文件，需挂载出来)挂载到/mnt下，再将已有的引导分区/dev/sda1挂载到新建的/mnt/boot目录

mount /dev/sda2 /mnt
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot



#### 选择中国镜像源

vim /etc/pacman.d/mirrorlist

Server = http://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
Server = http://mirrors.zju.edu.cn/archlinux/$repo/os/$arch



#### 安装基本包

安装最基本的`ArchLinux`包到磁盘上了。这是一个联网下载并安装的过程。

pacstrap /mnt base base-devel



#### 配置Fstab

生成自动挂载分区的`fstab`文件: 

genfstab -L /mnt >> /mnt/etc/fstab

查看输出生成的文件是否正确(/和/boot有无被正确挂载)：

cat /mnt/etc/fstab

> /dev/sda3           	/         	ext4      	rw,relatime	0 1
>
> /dev/sda1           	/boot     	vfat      	rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,utf8,errors=remount-ro	0 2



#### ==Chroot==

> `Chroot`意为`Change root`，相当于把操纵权交给我们新安装（或已经存在）的`Linux`系统，**执行了这步以后，我们的操作都相当于在磁盘上新装的系统中进行**。

arch-chroot /mnt

> 这里顺便说一下，如果以后我们的系统出现了问题，只要插入U盘并启动， 将我们的系统根分区挂载到了`/mnt`下（如果有`efi`分区也要挂载到`/mnt/boot`下），再通过这条命令就可以进入我们的系统进行修复操作。



#### 设置时区

ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
hwclock --systohc



#### 提前安装一些必要的软件

目前已经chroot到新的系统中，这个新系统只有一些最基本的包，为了装好后系统能更方便我们使用，需要提前安装一些利器，使用非常强大的包管理器——pacman

> 安装包的命令格式为`pacman -S 包名`，`pacman`会自动检查这个包所需要的其他包（即为依赖）并一起装上。

pacman -S vim dialog wpa_supplicant ntfs-3g networkmanager





#### 设置语言选项Locale

vim /etc/locale.gen

> 在文件中找到`zh_CN.UTF-8 UTF-8` `zh_HK.UTF-8 UTF-8` `zh_TW.UTF-8 UTF-8` `en_US.UTF-8 UTF-8`这四行，去掉行首的#号，保存并退出。

locale-gen
vim /etc/locale.conf  添加LANG=en_US.UTF-8



#### 设置主机名

1. vim /etc/hostname 填入自己的主机名，比如straw

2. vim /etc/hosts  在文末添加如下内容：

   ``` 
   127.0.0.1	localhost
   ::1		localhost
   127.0.1.1	straw.localdomain	straw
   ```

   

#### 设置root密码



### 解决引导问题

这里只记录UEFI引导的多系统的grub引导安装。

1. 因为是双系统，首先安装`os-prober`这个包，它可以配合`Grub`检测已经存在的系统，自动设置启动选项。
   pacman -S os-prober

2. 安装grub与efibootmgr两个包：pacman -S grub efibootmgr

3. 部署grub:
   grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=grub

4. 生成配置文件：grub-mkconfig -o /boot/grub/grub.cfg

5. 如果报错：

   > 如果报`warning failed to connect to lvmetad，falling back to device scanning.`错误。参照[这篇文章](https://www.pckr.co.uk/arch-grub-mkconfig-lvmetad-failures-inside-chroot-install/)，简单的方法是编辑`/etc/lvm/lvm.conf`这个文件，找到`use_lvmetad = 1`将`1`修改为`0`，保存，重新配置grub。
   >
   > 如果报`grub-probe: error: cannot find a GRUB drive for /dev/sdb1, check your device.map`类似错误，并且`sdb1`这个地方是你的u盘，这是u盘`uefi`分区造成的错误，对我们的正常安装没有影响，可以不用理会这条错误。

   __注：__经多次安装，这里配置引导时，最好现将/etc/lvm/lvm.conf文件里的use_lvmetad = 1`的`1`修改为`0`，然后再进行第3、4步，不然总会报错。

6. 检查：vim /boot/grub/grub.cfg 查看文件末尾的menuentry部分是否有Arch入口和windows入口。

7. 检查无误，则exit然后reboot了。

   





































### 安装后



#### 新建普通账号并授予sudo权限

- 同样先联网：dhcpcd或wifi-menu，然后ping某个域名测试。
- useradd -m -G wheel leave
  passwd leave
- 配置sudo: 
  pacman -S sudo
  visudo, 找到# %wheel ALL=(ALL)ALL，然后去掉#注释符，这意味着`wheel`组中的所有用户都可以使用`sudo`命令。
- 然后reboot, 之后用普通用户登录，后续操作可以使用sudo pacman -S 包名



#### 图形界面安装

- 我并没有安装专门的显卡驱动之类，只是装了Xorg.
- Xorg是Linux下的一个著名的开源图形服务，我们的桌面环境需要Xorg的支持。
- 偏爱gnome，如果还需要gnome自带的软件，可以额外安装gnome-extra。
- 安装好了桌面环境包以后，我们需要安装一个图形化的桌面管理器来帮助我们登录并且选择我们使用的桌面环境，推荐sddm。
- 并且需要设置开机启动sddm服务。

``` 
sudo pacman -S xorg
sudo pacman -S gnome gnome-extra
sudo pacman -S sddm
sudo systemctl enable sddm
```



#### 提前配置网络

> 到现在我们已经安装好了桌面环境，但是还有一件事情需要我们提前设置一下。由于我们之前使用的一直都是`netctl`这个自带的网络服务，而桌面环境使用的是`NetworkManager`这个网络服务，所以我们需要禁用`netctl`并启用`NetworkManager`：
>
> sudo systemctl disable netctl
> sudo systemctl enable NetworkManager （注意大小写）
>
> 同时你可能需要安装工具栏工具来显示网络设置图标（某些桌面环境已经装了，但是为了保险可以再装一下）：
>
> sudo pacman -S network-manager-applet

































#### ==图形界面美化==



##### 包管理器以及软件源

pacman使用的软件包来源都是官方的，但是arch拥有一个非常强大的用户库AUR(Arch User Repository)，为我们提供官方包之外的各种软件包，一些闭源的软件包也可以在上面找到。可以说`AUR`极大地丰富了软件包的种类与数量，并可以配合`yay`这样的工具为用户省下大量安装、更新软件包的时间。
`yay`实际上也是一个软件包，我们可以把它看成是对`pacman`的包装，它兼容`pacman`的所有操作，最大的不同是我们可以用它方便地安装与管理`AUR`中的包，下面的许多软件包都是在`AUR`库中的，也都是使用`AUR`来安装的。

- 安装yay

  > git clone https://aur.archlinux.org/yay.git
  > cd yay
  > makepkg -si

- yay使用(与旧的yaourt类似)：https://www.linuxdashen.com/arch-linux%E4%BD%BF%E7%94%A8yaourt%E5%8C%85%E7%AE%A1%E7%90%86%E5%99%A8%E8%BD%BB%E6%9D%BE%E5%AE%89%E8%A3%85aur%E8%BD%AF%E4%BB%B6%E5%8C%85

  

- 配置软件源：vim /etc/pacman.conf

  ``` 
  [archlinuxcn1]
  SigLevel = Optional TrustedOnly
  Server   =  http://repo.archlinuxcn.org/$arch
  
  [archlinuxcn2]
  #The Chinese Arch Linux communities packages.
  SigLevel = Optional TrustAll
  Server   =  https://mirrors.ustc.edu.cn/archlinuxcn/$arch
  ```

- **本机/etc/pacman.conf源配置参考**

  ``` 
  [archlinuxcn]
  SigLevel = Optional TrustedOnly
  #Server = http://mirrors.163.com/archlinux-cn/$arch
  Server = http://repo.archlinuxcn.org/$arch
  
  [core]
  Include = /etc/pacman.d/mirrorlist
  
  [extra]
  Include = /etc/pacman.d/mirrorlist
  
  [community]
  Include = /etc/pacman.d/mirrorlist
  
  ```

  而/etc/pacman.d/mirrorlist则仍保留安装arch时配置的中国源在最前：
  Server = http://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
  Server = http://mirrors.zju.edu.cn/archlinux/$repo/os/$arch

- 未尝试配置使用yay,因为初始的yay安装下载软件极慢我是修改了软件源然后各种日常软件都使用Pacman安装。

- 从aur源安装范例（未尝试）：

  - \#Sogoupinyin 
    搜狗拼音需要先编译一下安装包，再安装。 
    首先下载安装文件： 
    `～ sudo git clone https://aur.archlinux.org/fcitx-sogoupinyin.git` 
    再切换到下载目录里，执行： 
    `～ makepkg` 
    `～ sudo pacman -U xxxx.pkg.tar.xz` 
    现在还需要设置系统的环境变量为fcitx，可以使用kimtoy自动工具，也可以手工更改。使用kimtoy工具方法如下： 
    `～ sudo pacman -S kimtoy` 
    安装之后在命令行里输入‘kimtoy’打开，将fcitx设置为默认工具。

- 一些包查询命令：

  pacman -Ql pacman | grep bin  获取工具列表







##### 中文字体与中文输入法

> 中文字体推荐安装官方源中noto-fonts-cjk，中文输入法需要安装fcitx包与fcitx-im集合包，再加上一个中文支持包，可以到https://wiki.archlinux.org/index.php/fcitx#Chinese中挑选一个喜欢的包装上。

``` 
sudo pacman -S fcitx fcitx-im
pacman -S fcitx-sogoupinyin
sudo pacman -S fcitx-configtool
```

安装后不行的话，需要修改/etc/profile文件，在文件开头加入三行：

``` 
export XMODIFIERS="@im=fcitx"
export GTK_IM_MODULE="fcitx"
export QT_IM_MODULE="fcitx"
```



另外，可以额外安装一些字体：
sudo pacman -S adobe-source-han-sans-otc-fonts wqy-microhei wqy-zenhei wqy-microhei ttf-dejavu ttf-arphic-ukai ttf-arphic-uming



##### 双系统时间不同步

修改 win10 注册表
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation\
新建一项 DWORD 值 名为 “ RealTimeIsUniversal ”双击改成
值为 1





##### 安装日常软件

使用yay和pacman多尝试安装，包名如下：
netease-cloud-music, chromium, chrome, notepadqq, Synapse(桌面搜索), Yakuake, 
ntfs-3g, dosfstools, deepin-screenshot, calibre(电子书制作神器), 



- \#Atom 
  这是一个好用的文本编辑器，我用它来写Markdown和python代码，安装只需要执行如下的安装命令： 
  `～ sudo pacman -S atom` 
  Atom有一些好用的插件，我安装了atom-beautify,markdown-preview-plus,markdown-table-editor,markdown-to-pdf,markdown-img-paste,kite,script，这些用于markdown写作和python代码的编写和调试。

- \#Proxychains 
  Proxychains简直是一个和SS配合使用的神器，有了这个软件，凡是能在命令行里启动的软件都可以通过代理服务器。这带来的好处很多，我最喜欢的就是配合下载命令使用，这样可以使得下载一些GitHub上文件或者其他国外服务器文件速度快多了。再者，telegram机器人的一些有趣的开发需要国外服务器，但是我现在只要有一个能访问外网的SS账号就可以了，可以把本机电脑变成一个“国外的服务器”。 
  安装命令只需要执行： 
  `～ sudo pacman -S proxychains-ng` 
  以后要使用时，直接proxychains+命令，例如： 
  `～ proxychains wget https://xxxxxx`



##### 主题图标

- gnome-tweak-tool

  - 敲gnome-tweaks唤醒，更多的GNOME Shell Extensions参考此网站下载：https://extensions.gnome.org/

  - 此为在web浏览器中在线安装扩展的方式(本人之前手动安装扩展没效果)，主要是安装一个浏览器附加组件即可，像谷歌浏览器就可以在应用商店里找到GNOME Shell integration这个插件。
  - 接下来，安装一个主机连接器chrome-gnome-shell,后续就可以在上面那个网址里轻松愉快地下载安装gnome桌面的扩展了，有很多非常有用的功能：
    Dash to Dock (类似于 MAC dock 程序栏)、system-monitor (显示系统信息)、Coverflow Alt-Tab (Alt + Tab 3D 切换效果)、Simple net speed (显示网速)、User Themes (使用用户自定义主题)、Unite (合并菜单栏和顶部栏) 、Screenshot Tool...

- gtk-theme-arc-git主题

- numix-circle-icon-theme-git图标

- archibold login-background /home/leave/Pictures/fanxing.jpg（测试无用）

  

##### gdm背景






##### 虚拟机







##### 代理配置

1. 终端直接运行命令

   ``` 
   export http_proxy=http://proxyAddress:port
   ```

   补充：

   如果代理服务器需要登陆，这时可以直接把用户名和密码写进去

   ```
   http_proxy=http://userName:password@proxyAddress:port
   ```

   如果你用的是ss代理，在当前终端运行以下命令，那么`wget` `curl` 这类网络命令都会经过ss代理:

   ``` 
   export ALL_PROXY=socks5://127.0.0.1:1080
   ```

2. shell配置文件

   把代理服务器地址写入shell配置文件`.bashrc`或者`.zshrc`

   直接在`.bashrc`或者`.zshrc`添加下面内容

   ```
   export http_proxy="http://localhost:port"
   export https_proxy="http://localhost:port"
   ```

   以使用shadowsocks代理为例，ss的代理端口为`1080`,那么应该设置为

   ```
   export http_proxy="socks5://127.0.0.1:1080"
   export https_proxy="socks5://127.0.0.1:1080"
   ```

   或者直接设置ALL_PROXY

   ```
   export ALL_PROXY=socks5://127.0.0.1:1080
   ```

   `localhost`就是一个域名，域名默认指向 `127.0.0.1`，两者是一样的。

   然后`ESC`后`:wq`保存文件，接着在终端中执行
   `source ~/.bashrc`

   或者退出当前终端再起一个终端。 这个办法的好处是把代理服务器永久保存了，下次就可以直接用了。

   或者通过设置alias简写来简化操作，每次要用的时候输入`setproxy`，不用了就`unsetproxy`。

   ```
   alias setproxy="export ALL_PROXY=socks5://127.0.0.1:1080"
   alias unsetproxy="unset ALL_PROXY"
   alias ip="curl -i http://ip.cn"
   ```

3. 利用proxychains在终端使用socks5代理

   推荐使用`proxychains-ng`包进行命令行代理：

   安装`proxychains-ng`包后编辑`/etc/proxychains.conf`文件（需`root`权限）

   到文件末尾找到`ProxyList`项，按示例添加本地代理。

   使用方法：在需要代理的命令钱加上proxychains4，如：proxychains4 wget http://xxx.com/xxx.zip

4. 



#### 安装软件过程中所遇疑难

##### 代理环境下安装yay

1. root设置代理

   ``` 
   [root@straw yay]# reboot
   
   Last login: Tue Sep 11 00:00:58 2018 from 192.168.64.1
   [root@straw ~]# pacman -S dialog
   resolving dependencies...
   looking for conflicting packages...
   
   Packages (1) dialog-1:1.3_20190211-1
   
   Total Download Size:   0.18 MiB
   Total Installed Size:  0.43 MiB
   
   :: Proceed with installation? [Y/n] y
   :: Retrieving packages...
   error: failed retrieving file 'dialog-1:1.3_20190211-1-x86_64.pkg.tar.xz' from mirrors.tuna.tsinghua.edu.cn : Connection timed out after 10001 milliseconds
   error: failed retrieving file 'dialog-1:1.3_20190211-1-x86_64.pkg.tar.xz' from arch.serverspace.co.uk : Connection timed out after 10001 milliseconds
   ^C
   Interrupt signal received
   
   [root@straw ~]# echo $http_proxy
   
   [root@straw ~]# export http_proxy=http://cmproxy.gmcc.net:8081
   [root@straw ~]# pacman -S dialog                              
   resolving dependencies...
   looking for conflicting packages...
   
   Packages (1) dialog-1:1.3_20190211-1
   
   Total Download Size:   0.18 MiB
   Total Installed Size:  0.43 MiB
   
   :: Proceed with installation? [Y/n] y
   :: Retrieving packages...
    dialog-1:1.3_2019021...   179.8 KiB   509K/s 00:00 [###########################] 100%
   (1/1) checking keys in keyring                      [###########################] 100%
   (1/1) checking package integrity                    [###########################] 100%
   (1/1) loading package files                         [###########################] 100%
   (1/1) checking for file conflicts                   [###########################] 100%
   (1/1) checking available disk space                 [###########################] 100%
   :: Processing package changes...
   (1/1) installing dialog                             [###########################] 100%
   :: Running post-transaction hooks...
   (1/1) Arming ConditionNeedsUpdate...
   [root@straw ~]# 
   ```

2. git clone报ssl证书错误

   ``` 
   [root@straw ~]# proxychains4 git clone https://aur.archlinux.org/yay.git
   [proxychains] config file found: /etc/proxychains.conf
   [proxychains] preloading /usr/lib/libproxychains4.so
   [proxychains] DLL init: proxychains-ng 4.13
   Cloning into 'yay'...
   [proxychains] DLL init: proxychains-ng 4.13
   [proxychains] Strict chain  ...  10.244.155.188:1080  ...  aur.archlinux.org:443  ...  OK
   fatal: unable to access 'https://aur.archlinux.org/yay.git/': SSL certificate problem: certificate is not yet valid
   [root@straw ~]# ^C
   ```

   解决方法：https://stackoverflow.com/questions/19045556/git-clone-https-ssl-error

   ``` 
   [root@straw ~]# git config --global http.sslVerify false
   [root@straw ~]# proxychains4 git clone https://aur.archlinux.org/yay.git
   [proxychains] config file found: /etc/proxychains.conf
   [proxychains] preloading /usr/lib/libproxychains4.so
   [proxychains] DLL init: proxychains-ng 4.13
   Cloning into 'yay'...
   [proxychains] DLL init: proxychains-ng 4.13
   [proxychains] Strict chain  ...  10.244.155.188:1080  ...  aur.archlinux.org:443  ...  OK
   [proxychains] DLL init: proxychains-ng 4.13
   remote: Enumerating objects: 240, done.
   remote: Counting objects: 100% (240/240), done.
   remote: Compressing objects: 100% (171/171), done.
   [proxychains] DLL init: proxychains-ng 4.13
   remote: Total 240 (delta 67), reused 240 (delta 67)
   Receiving objects: 100% (240/240), 49.50 KiB | 299.00 KiB/s, done.
   Resolving deltas: 100% (67/67), done.
   [proxychains] DLL init: proxychains-ng 4.13
   ```

   

3. root安装go, kering报错

   ``` 
   [root@straw ~]# pacman -S go
   resolving dependencies...
   looking for conflicting packages...
   
   Packages (1) go-2:1.12-1
   
   Total Download Size:   121.32 MiB
   Total Installed Size:  473.11 MiB
   
   :: Proceed with installation? [Y/n] y
   :: Retrieving packages...
    go-2:1.12-1-x86_64        121.3 MiB  1042K/s 01:59 [###########################] 100%
   (1/1) checking keys in keyring                      [###########################] 100%
   downloading required keys...
   error: key "E742683BA08CB2FF" could not be looked up remotely
   error: required key missing from keyring
   error: failed to commit transaction (unexpected error)
   Errors occurred, no packages were upgraded.
   [root@straw ~]# pacman -Ql go
   error: package 'go' was not found
   [root@straw ~]# 
   ```

   解决方法：reinstalling archlinux-keyring

   sudo pacman -S archlinux-keyring

4. leave普通用户配置完代理却无法下载go

   ``` 
   [leave@straw yay]$ makepkg -si
   ==> Making package: yay 9.1.0-1 (Tue 11 Sep 2018 06:14:04 AM CST)
   ==> Checking runtime dependencies...
   ==> Checking buildtime dependencies...
   ==> Installing missing dependencies...
   resolving dependencies...
   looking for conflicting packages...
   
   Packages (1) go-2:1.12-1
   
   Total Download Size:   121.32 MiB
   Total Installed Size:  473.11 MiB
   
   :: Proceed with installation? [Y/n] y
   :: Retrieving packages...
   error: failed retrieving file 'go-2:1.12-1-x86_64.pkg.tar.xz' from mirrors.tuna.tsinghua.edu.cn : Connection timed out after 10001 milliseconds
   ^C^C
   Interrupt signal received
   
   
   ==> ERROR: Aborted by user! Exiting...
   
   ```

   配置.bashrc后依旧不行，只好用proxychains4:

   ``` 
   [leave@straw ~]$ sudo proxychains4 pacman -S go
   [proxychains] config file found: /etc/proxychains.conf
   [proxychains] preloading /usr/lib/libproxychains4.so
   [proxychains] DLL init: proxychains-ng 4.13
   resolving dependencies...
   looking for conflicting packages...
   
   Packages (1) go-2:1.12-1
   
   Total Download Size:   121.32 MiB
   Total Installed Size:  473.11 MiB
   
   :: Proceed with installation? [Y/n] y
   :: Retrieving packages...
   [proxychains] Strict chain  ...  10.244.155.188:1080  ...  mirrors.tuna.tsinghua.edu.cn:80  ...  OK
    go-2:1.12-1-x86_64        121.3 MiB  1105K/s 01:52 [###########################] 100%
   (1/1) checking keys in keyring                      [###########################] 100%
   (1/1) checking package integrity                    [###########################] 100%
   error: go: signature from "Morten Linderud <morten@linderud.pw>" is invalid
   :: File /var/cache/pacman/pkg/go-2:1.12-1-x86_64.pkg.tar.xz is corrupted (invalid or corrupted package (PGP signature)).
   Do you want to delete it? [Y/n] y
   error: failed to commit transaction (invalid or corrupted package (PGP signature))
   Errors occurred, no packages were upgraded.
   [leave@straw ~]$ 
   ```

   但是获取到的依赖软件go，是损坏的，所以没装成功。
   该Arch是1808版的，至今没有pacman -Syu，估计是这个原因。





##### 谷歌浏览器占cpu

dstat -cdnpmgs --top-bio --top-cpu

> https://bbs.archlinuxcn.org/viewtopic.php?id=5852
>
> 1. 试了有效：
>
>    - 关闭chrome
>
>    - ```
>      cd /home/$USER/.local/share/keyrings/
>      mv 默认密钥环.keyring 默认密钥环.keyring.old
>      ```
>   ```
> 
>   ```
>
>    - 打开chrome，坐等同步，期间因为同步gnome-keyring-daemon的cpu稍微会高一点
>
> 2. “Ugly fix”，没试：删除 gnome-keyring 包，去掉 默认密钥环.keyring 的执行权限
>
> 老实说，不明白 chrome 为啥把密码保存在gnome-keyring中。
>
> ```
> 
> ```



##### 锁屏快捷键无效

Ubuntu16.04 桌面环境通过Ubuntu server和后安装的Gnome3 桌面环境实现，安装完以后发现锁定屏幕快捷键无效，系统设置=>键盘=>快捷中 锁屏快捷键已经存在Super+L
我通过键盘怎么实验也不行，在网上查找说快捷键是Ctrl+Alt+L，实验了好几次也不行，在系统设置=>键盘=>快捷中把快捷键设置成Ctrl+Alt+L也不行，在网上无意间找到
通过安装gnome-screensaver（屏幕保护程序可以解决），程序安装完重启真的好了。























#### 系统备份

























