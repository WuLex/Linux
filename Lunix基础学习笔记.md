#Linux教程
##Linux简介
Linux是一套免费使用和自由传播的类Unix系统。是一个基于POSIX和Unix的**多用户、多任务、多线程、多CPU**的操作系统。  
  支持32位和64位硬件  
**Linux VS Windows**   
1. Linux主要应用在服务器上，而桌面操作是Windows  
2. 同样内存，linux上运行速度更快，因为windows会存储一些图形化界面的数据占了部分内容  
3. linux开源免费。windows收费  
4. linux对用户的权限管理严格  
5. windows对用户没有要求，普通用户可以所以操作，安全性较低。而linux对用户要求较高，规避了一些风险  
6. linux系统安全性更高，没有漏洞、木马等的侵害  
##Linux安装  
以CentOS 6.8为例  
**版本选择**  
网易镜像：http://mirrors.163.com/centos/6/isos/  
1. binDVD：普通安装版本，需安装到本地计算机硬盘，bin版是最完整的版本，一般比较大，因为包含了大量常用软件。安装时无需在线下载。若是安装在虚拟机中学习，首选。  
DVD1：基本系统+部分软件包  
DVD2：更多的软件包  
2. liveDVD：光盘安装版。  
3. liveCD：相比liveDVD，是个精简的光盘CentOS系统，体积更小，便于维护。  
4. mininal版：迷你版，精简了更多东西。虚拟机学习，不推荐使用。因不带一些基本的软件，使用起来比较麻烦。  
5. netinstall：网络安装版，不推荐。   
**通过SecureCRT连接虚拟机上的Linux**  
>1. 通过ifconfig获取操作系统的ip地址  
>2. 在SecureCRT上新建连接，在connection下新建name，默认选择SSH2（安全外壳协议Secure Shell缩写）。  
>3. 在SSH2 下输入hostname (即连接系统的ip地址)，输入登录系统的用户名连接，输入密码即可  


##系统启动过程  
###启动过程分五个阶段：  
* 内核的引导  
* 运行init  
* 系统初始化  
* 建立终端  
* 用户登录系统  
### Linux系统7个运行级别  
* 0：系统停机状态，默认不能设为0，否则不能启动  
* 1：单用户工作状态，root权限。用于系统维护，禁止远程访问  
* 2：多用户状态（没有NFS，Network File System ）  
* 3：完全的多用户状态（有NFS）。登录后进入控制台命令行模式  
* 4：系统未使用，保留  
* 5：X11控制台。登陆后进入图形GUI模式  
* 6：系统正常关闭并重启。默认运行级别不能是6，否则不能正常启动   
###Linux关机  
正确的关机流程sync>shutdown>reboot>halt  
关机指令shutdown。可通过man shutdown查看帮助文档   
**给用户添加sudo权限**    
>1. 由普通用户进入超级用户模式（即进入root模式）。在普通模式下输入'su-'，然后输入root密码，回车，进入超级用户模式   
>2. 输入命令'visudo' 进入编辑模式。（编辑sudo的配置文件/etc/sudoers）  
>3. 找到'root ALL=(ALL) ALL'(可能当前页找不到，一直回车)在该行下面添加 Lilybo ALL=(ALL) ALL  
>4. 保存退出：w(保存)，exit(退出)  
###关机相关命令
* sync 将数据由内存同步到硬盘中（关闭或重启前一定要执行）  
* shutdown -h 10 'this server will shutdown after 10mins'  10分钟后系统关机，信息会显示在登录用户的当前屏幕 (h是halt缩写，停止的意思)   
* shutdown -h now 立马关机    
* halt   关闭系统   等同于上面命令和poweroff  、init 0（普通用户用命令sodu init 0）
* shutdown -h 20:25 系统会在20:25关机  
* shutdown -h +10 十分钟后  
* shutdown -r now 系统立马重启（reboot）    
* reboot 重启，等同意上面命令、init6  
* shutdown -r +10 系统10分钟后重启    
* shutdown -c 取消正在进行的重启  
* shutdown -k 10 并非真正关机，只是显示警告信息 。系统将在10分钟后关机  
##Linux系统目录结构 
**ls和ls / 区别**  
>ls 是文件列表命令，显示当前目录下的所有文件  
>ls / '/'表示根目录的意思，该命令意思显示根目录下的文件  

* /bin bin是banary（二进制）缩写，该目录显示最常用的命令  
* /boot 存放启动linux是的一些核心文件，包括镜像文件  
* /dev device(设备)缩写。该目录存放的是linux的外部设备。访问设备和访问文件的方式是相同的  
* /etc 存放所有系统管理所需要的配置文件和子目录   
* /home 用户主目录。每个用户都有一个自己的目录。一般目录名已用户账号命名  
* /lib 存放系统最基本的动态链接共享库。作用类似于window下的DLL文件。几乎所有的应用文件都需要用到这些共享库  
* /lost+found 一般是空的。当系统非法关机后，这里会存放一些文件。  
* /media linux会自动识别一些设备，如U盘、光驱等。当识别后，linux会把识别的设备挂载在该目录下  
* /mnt 让用户临时挂载别的文件系统。我们可以将光驱挂载在该目录下，然后进入该目录就可以查看光驱里的内容了  
* /opt 给主机额外安装软件所摆放的目录。如数据库等。默认为空  
* /proc 该目录是虚拟目录。它是系统内存的映射，可以通过访问该目录获取系统信息 。该目录的内容不再硬盘上，而在内存里。可以直接修改里面的某些文件。  
* /root 该目录是系统管理员，也称超级权限者的用户目录  
* /sbin S是super user的意思。这里存放系统管理员使用的系统管理程序  
* /selinux 该目录是Rethat/CentOS特有的。Selinux是一个安全机制，类似window下的防火墙，该目录就是存放selinux相关文件  
* /srv 存放服务启动后需要读取的数据  
* /sys  该目录安装文件系统sysfs  
* /tmp 存放一些临时文件  
* /usr 非常重要的目录。用户的很多应用程序和文件都放在这里。类似window下的program files  
* /usr/bin 系统用户使用的应用程序  
* /usr/sbin 超级用户使用的比较高级的管理程序  
* /usr/src 内核源代码默认放置的目录  
* /var 存放不断扩充的东西。习惯将经常被修改的目录放在该目录下，包括各种日志文件  
**几个比较重要不能修改的目录**  
* /etc 系统配置文件，更改后可能系统不能启动  
* /bin ,/sbin,/usr/bin,/usr/sbin  
* /var 非常重要的目录。系统上跑的程序的日志存在该目录下。在/var/log下  
##Linux忘记root密码解决办法
###通过linux系统直接重置密码  
1. 重启linux,在3秒内回车，进入GRUB界面  
2. 选择操作系统，输入e进入  
3. 向下选择“kerner”内核那一行，输入e   
4. 在最后一行quiet 后面空格，然后输入single，回车，此时回到选择kerner 界面  
5. 按b，进入单用户模式，在这里修改密码  
6. 输入命令passwd  
7. 输入新密码，回车后，再输入一次密码  
8. init 6重启系统完成设置  
###记得root密码，通过远程连接修改密码 
1. 普通用户登录远程连接时，首先切换到root用户，输入命令su （切换到root）  
2. 输入root登录密码  
3. 进入到root下，输入passwd ，输入新密码，回车再次输入新密码。  
4. 成功后，切回普通用户，su lilybo    
###普通用户的密码忘记   
1. 进入管理员模式，su
2. 在root下输入命令：passwd lilybo,回车  
3. 输入新密码，确认密码。成功  
##Linux文件基本属性    
可以通过命令ll、ls-l来显示一个文件的属性、以及文件所属用户和组  
drwxr-xr-x  （10个字符组成，第一个表示文件类型，后面每3个一组，表示相应权限） 
   
1.  第0位。即第一个字符代表文件类型： [d]目录、[-]文件、[/]链接、[b]表示装置文件里面可供储存的接口设备（可随机存取装置）、[c]表示装置文件里面的串行端口设备，如键盘、鼠标（一次性读取装置）   
2. 以 [rwx] 组合。[r]表示read,可读；[w]write,可写；[x]execute，可执行。当没有选项时，就用[-]代替  
3. 1~3位，确定属主（文件所有者）拥有的该文件权限  
4. 4~6位，确定属组（所有者同组用户）拥有的权限  
5. 7~9位，确定其他用户对该文件的权限 
 
###更改文件属性  
* chgrp：更改文件属组(变更文件或目录的权限)  
  -[R] 属组名 文件名 R表示递归更改文件属组。在更改某个目录文件的属组时，该目录下的所有文件的属组都会更改   
* chown：更改文件属主，也可以同时更换属组  
  -[R] 属主名 文件名  
  -[R] 属主名：属组名 文件名  
  chown lilybo install.log 将install.log文件的拥有者改为lilybo   
  chown lilybo：lilybo install.log 将install.log的文件的拥有者和属组都改为lilybo  
* chmod：更改文件9个属性  
  1. 数字法  chmod -[R] xyz 文件或目录  
     r：4  w:2 x:1   
     [-rwxrwx---]  代表rwx:4+2+1=7 rwx:4+2+1=7  ---:0    最后权限数字是770（即xyz）  
     如：chmod 770 install.log   
  2. 符号类型   
     9个权限分别是user（u）、group（g）、others（o）三种身份 。 all(a)代表所有身份  
     chmod  u/g/o/a +(增加)/-(去除）/=(设定)  r/w/x
       
## Linux文件与目录管理  
* 绝对路径：绝对路径的写法，由根目录“/”写起。如：/usr/share/doc  
* 相对路径：不是由“/”写起。如从/usr/share/doc 到/usr/share/man 。可以用 cd ../man.  
###处理目录的常用命令  
#### ls (list 列出目录 )  
  语法：ls [目录名称]

 *  ls -a 列出文件下所有文件，包括已‘.’开头的隐藏文件。和“.”“..”.a 代表all    
 *  ls -A 列出除了“.”和“..”以外的文件
 *  ls -l 或ll 列出目录下文件的详细信息  
 *  ls -s 在每个文件的后面打印文件的大小   
 *  ls -S 以文件大小排序显示 
 *  ls -t 按时间排序显示文件  
 *  ls -R [文件名]（recursion递归）将目录下所有子目录的文件都列出来    
 *  ls -d 仅列出目录本身。而不是列出目录下的文件
 *  ls -al 列出当前目录下的所有文件（包含隐藏文件）的详细信息
#### cd (切换目录 change directory) 
* 使用绝对路径切换目录：cd /usr/share/doc
* 使用相对路径切换目录：cd ../man  
  
####pwd (显示目前所在目录 print working directory)  
#### mkdir(创建新目录 make directory即创建文件夹) 
* mkdir -p  文件名 创建目录时将上级目录一起创建起来    
  例：mkdir -p  test/test1/test2  直接创建三个目录     
* mkdir -m 权限  文件名 创建文件时，直接配置权限 
  例：mkdir -m 711 test2   
**创建文件命令 touch 文件名**   

#### rmdir (删除空的目录 remove directory) 
* rmdir -p 目录名 连同上一级空的目录一起删除。p :parents  
  例：rmdir -p test1/test2/test3  连同test3的上级空目录一起删除  
  rmdir test1/test2/test3  只会删除目录test3
  
#### cp (复制文件或目录)  
语法： cp 来源档（source） 目标档（destination）
  
* cp -a 相当于-pdr.pdr说明参考以下（常用）   
  例：想把/tmp/test5里面的文件和文件夹复制到 /tmp/test4  
     cp -a /tmp/test5/* /tmp/test4    
     想把/tmp/test5目录复制到/tmp/test4 下  
     cp -a /tmp/test5 /tmp/test4 (结果：/tmp/test4/test5)
* cp -d 若来源档为连结档的属性（link file ）,则复制连结档属性，而非文件本身  
* cp -f 强制（force）的意思。若目标文件已经存在，且无法打开。则移除后，再尝试一次 
* cp -i 若目标档已经存在时，再覆盖时会先询问动作的进行（常用）
* cp -l 进行硬式连接的连接档创建，而非复制文件本身  
* cp -p 连同文件的属性一起复制过去，而非使用默认属性（备份常用）
* cp -r 递归持续复制，用于目录的复制行为。（常用）
* cp -s 复制成为符号连接档（symbolic link），即【捷径】文件 
* cp -u 若destination 比source 旧。才升级destination
  
#### rm(移除文件或目录)
* rm -f (force)直接强行删除，不做任何提示  
* rm -r 向下递归（recursive），不管有多少目录，一起删除   
  例：清空文件夹/tmp/a ：rm -rf /tmp/a/*  结果，保留a目录，清空下面的所有文件，文件夹  
     删除整个a目录。：rm -rf /tmp/a  
* rm -i 删除前询问是否删除   

#### mv (移动文件与目录，或修改名称)  
语法 mv 源文件 目标文件 
 
* mv -f 
* mv -i 
* mv -u 若目标文件已经存在，且source 比较新，才会升级（update）
  例：mv test test1  

###Linux 文件内容查看 
####cat (由第一行开始显示文件内容)

* cat -A 相当于-vET整合，可列出一些特殊字符  
* cat -b 列出行号。仅针对非空白行，空白行不标记（number-nonblank）
* cat -n 列出行号，包括空白行也会有行号
* cat -E 将结尾的断行字符$显示出来（show ends）
* cat -T 将[tab]键已^|显示出来  
* cat -v 列出一些看不出来的特殊字符 
####tac (从最后一行开始显示) 
是cat的倒写 
#### nl (显示行号 number of lines)
nl 文件：默认只列出非空行号
* nl -ba:同cat -n 

#### more (一页一页翻动) 
语法：more 文件名

* space 空格 ，表示翻页  
* enter 回车，表示一行一行显示 
* /a    表示向下搜索a
* ：f   显示当前文件名和以显示的行数
* q    退出
* b    往回翻页  

#### less (与more类似)
* ?a  向上查找a
区别：less 多了向上查询  

#### head（取出文件前面几行）
* head 文件 默认显示10行
* head -n 20 文件  表示显示20行 

#### tail(显示后几行)
* tail 文件 默认显示文件后10行 
* tail -n 20 文件 表示显示文件后20行

##Linux 用户和用户组管理
### Linux系统用户账号管理
####添加账号（useradd）
语法：useradd 选项 用户名   
选项：    

* -c (comment)指定一段注释性描述 
* -d 目录 指定用户主目录(home-dir)。如果主目录不存在，可以同时使用-m，创建主目录 
* -g 用户组 指定用户的用户组
* -G 用户组，用户组  指定用户的附加组
* -s shell文件 指定用户的登录shell
* -u 用户号 指定用户的用户号
* -m 创建用户住目录  

添加用户是在/etc/passwd 文件中增加一条用户记录。同时更新/etc/shadow,/etc/group

  
#### 删除账号（userdel）   
语法：userdel 选项 用户名  

* -r 表示联通用户的主目录一起删除  
 userdel -r lilybo 表示删除lilybo账户，并且删除其主目录  
 
####修改账号（usermod）
usermod 选项 用户名
命令同useradd 
#### 用户密码的管理（passwd） 
语法：passwd 选项 用户名（如果不写用户名，默认修改当前用户口令）

* -l 锁定口令（lock），即禁用账号  
* -u 口令解锁（unlock）
* -d 删除口令，即用户无口令
* -f 强制用户下次登录说修改密码 
普通用户：passwd 回车，输入原密码和新密码，修改当前用户口令
超级用户：passwd username  回车，直接输入用户的新密码。

### Linux系统用户组管理
Linux下的用户属于与他同名的用户组，这个用户组，在创建用户的时同时创建
#### 增加新的用户组（groupadd）
语法：groupadd 选项 用户组名  

* -g 标识号 指定新用户组的组标识号（GID  group identification）  
 注：UID  用户唯一标识  
* -o 一般与-g同时使用。表示组标识号可以重复（non-unigue）   
groupadd -g 101 group 向系统中增加新组group，且组标识号

####删除用户组（groupdel）
语法：groupdel 组名
####修改用户组 （groupmod）
语法：groupmod 选项 用户组   

* -g 、-o 用法同添加组
* -n 新用户组名 更改用户组名
groupmod -g 1000 -n group3 group2 
将group2的标识号改为1000，组名改为group3

#### 如果一个用户属于多个用户组，那么用户可以在用户组中随时切换，以便具有不同用户组的权限
用户在登录后可以使用命令：newgrp切换到其他用户组
newgrp root 切换到root用户组
###与用户账号有关的系统文件
#### /etc/passwd 为用户管理工作涉及的最重要的一个文件
Linux每一个用户对应/etc/passwd一行记录，记录了用户的一些基本属性
cat /etc/passwd 显示文件内容
lilybo:x   :500       :507    :CentOS    :/home/lilybo:/bin/bash 分别表示：  
用户名：口令：用户标识号：组标识号：注释性藐视：主目录       ：登录Shell

* “用户名”是代表用户账号的字符串 
通常不超过8个字符，并且由大小写字符和/和数字组合。登录名中不能有：，因为冒号在这里是分隔符  
为了兼容起见，登录名最好不包括“.”字符，最好不适用连字符-和+开头  
* “口令”一些系统中，存放着加密口令  
 * 虽然这个字段存放的是加密后的口令，但是毕竟/etc/passwd这个文件对所有用户都可读，存在安全隐患。  
 * 所以，现在很多Linux系统（如SVR4）都使用shadow技术。把真正加密后的口令放在/etc/shadow中，而/etc/passwd中该字段存放的只是x 或*  
* “用户标识号”是一个整数，系统内部用它来标识用户  
 * 一般情况下与用户名是一一对应的。如果几个用户名的用户标识号是一样的，系统内部将他们视为同一用户，但是他们可以有不同的口令（密码）、不同的主目录、不同的登录Shell等  
 * 通常用户标识号的取值范围为0~65535。0是超级用户的标识号。1~99由系统保留，作为管理账号。一般用户从100以上取值。在Linux中普通用户标识号从500开始取值
* “组标识号”记录的是用户所属用户组  
它对应/etc/group文件中的一条记录  
* “注释性描述”记录的用户的一些个人信息  
没有统一格式
* “主目录”，也就是用户的起始工作目录  
是用户登录系统后所处的目录了。在大多数系统中，各用户的主目录都没组织在同一个特定目录下，而用户主目录的名称，就是该用户的登录名。各用户对自己的主目录有r\w\x权限。 
* “登录Shell”。用户登陆后，要启动一个进程，负责将用户的操作传个内核。这个进程是用户登录后，运行的命令解释器或某个特定的程序。即Shell  
* 系统中有一类用户称为伪用户（psuedo users） 
这些用户在/etc/passwd文件中也占有一条记录。但是不能登录，因为登录Shell为空。他们的存在主要是方便系统管理。  
常见的伪用户：  
 * bin 拥有可执行的用户命令文件  
 * sys 拥有系统文件 
 * adm 拥有账户文件  
 * uucp UUCP使用 
 * lp lp或lpd子系统使用
 * nobody NFS使用   
 
####/etc/shadow中的记录行与/etc/passwd中一一对应。它由pwconv命令根据/etc/passwd中的数据自动生成的  
lilybo:$SWWNOTGNWWERGWTG:17226:0:99999:7:::  

* 登录名 
* “口令”存放加密后的用户口令。如果含有不属于{./0-9A-Za-z}中的字符。则对应的用户不能登录  
* “最后一次修改时间”表示从某个时刻起，到用户最后一次修改口令的天数。  
* “最小时间间隔”指两次修改口令之间所需的最小天数  
* “最大时间间隔”  
* “警告时间”指系统开始警告用户到用户密码正式失效的天数 
* “不活动时间”只用户没有没有登录活动但账号仍保持有效的最大天数  
* “失效时间”如果使用该字段，就要给出相应账号的生存期。期满后，该账号就不再是一个合法的账号，也就不能登录了 
* “标志” 

####/etc/group用户组的所有信息存放在该文件中 
lilybo：x:500：
组名：口令：组标识号：组内用户列表
###批量添加用户

1. 先添加用户文件 。每一列按照/etc/passwd格式写。注意所有用户的用户名、UID、宿主目录搜不可以相同。

 * touch user.txt (新建文件)
 * vim user.txt (编辑文件，添加下面内容) 
 * 保存退出   
 user001:x:600:100:user:/home/user001:/bin/bash  
 user002:x:601:100:user:/home/user002:/bin/bash  

2. 添加密码文件。参照/etc/shadow 
 
 * touch passwd.txt(新建密码文件)
 * vim passwd.txt (编辑密码文件，添加如下内容)  
  user001:1  
  user002:2  
 * 保存退出
3. 通过批量添加用户工具：newusers 导入用户文件
 * newusers < user.txt
4. 通过批量更新用户口令工具：chpasswd 导入密码文件
 * chpasswd < passwd.txt
5. 至此用户添加完成， 添加的用户可以登录系统 （基于用户创建时登录shell 为/bin/bash）
##Linux磁盘管理
####df（ disk free 列出文件系统的整体磁盘使用量）
语法：df [-ahikHTm] [目录或文件名]  
df  后面不加任何选项，默认会将系统内所有的（不含特殊内存的文件系统和swap）系统文件（即磁盘）以1K的容量列出来

* -a 列出所有的文件系统，包括系统特有的/proc等文件系统
* -k 以KB的容量显示各文件系统
* -m 以M的容量显示各文件系统
* -h （human-readable）以人们交易阅读的G、M、K等格式自行显示(亲测，好用)
* -H 以M=1000k代替M=1024k等进位方式
* -T 显示文件系统类型（type）
* -i（inode）不用硬盘容量，而以inode等数量来显示
####du（disk usage（使用）查看文件和目录磁盘使用量）
语法：du [-ahskm] 文件或目录名称
du 后面不加任何选项和文件名时，默认显示当前目录下面的文件与目录所占用的磁盘空间

* -a 列出所有的文件与目录容量，默认只显示当前目录下的子目录大小
* -h （human readable）
* -s （summarize）列出总量，而不列出某个目录占用情况
* -S 不包括子目录下的总计
* -k （默认显示的容量以k为单位）
* -m
* -s /* 查看根目录下没有目录所占容量

####fdisk(磁盘分区)
语法：fdisk [-l] 装置名称
* -l 输出后面装置的所有分区内容，若仅有 fdisk -l ，则显示整个系统内能搜到的装置的分区内容  
例：df /  找到根目录所在磁盘  
   fdisk /dev/sda   
   回车后，输入m 显示帮助命令
   最后q是直接退出，w是保存退出
####mkfs（make filesystem 磁盘格式化）
语法：mkfs [-t 文件系统格式] 装置文件名
磁盘分割完成后就要进行文件系统的格式化
输入命令mkfs 按tab键，显示mkfs支持的文件格式  

* -t 文件系统格式（ext2、ext3、vfat）
####fsck（filesystem check磁盘检查）
语法：fsck [-t 文件系统] [-ACay] 装置名称 

* -t 
* -s 依序一个一个的执行fsck来检查
* -A 对/etc/fstab中所有列出来的分区（partition）做检查
* -C 显示完整的检查进度
* -d 打印出e2fsck的debug结果
* -p 同时有-A条件时。同时有多个fsck 一起执行
* -R 同事有-A条件时，省略/不检查
* -V 显示显示模式
* -a 如果检查有错则自动修复
* -r 如果检查有错，则有使用者觉回答是否修复
####mount、umount（磁盘挂载与卸载）
挂载语法：mount [-t 文件系统] [-L label名] [-o 额外选项] [-n] 装置文件名 挂载点
**挂载解释**  
在linux系统中，整个文件系统就有一个顶级的根目录（/）。所有物理磁盘都是根目录下的子目录。  
当我们新建分区后，要将该分区挂载在一个新创建的目录下面，成功后，访问该目录就可以访问添加上的硬盘或分区 
 
例：用默认的方式将新创建的/dev/hdc6分区，挂载到目录/mnt/hdc6上  
   mkdir /mnt/hdc6  
   mount /dev/hdc6  /mnt/hdc6  
磁盘卸载语法：umount [-fn] 装置文件名或挂载点

* -f 强制卸载。
* -n 不升级/etc/mtab情况下卸载 
例：umount /dev/hdc6  

##Linux vi/vim
###vi/vim的使用
vim共分三种模式：  
vi file ---命令模式---i/o/a---输入模式---esc---命令模式---：---底线命令模式---wq回车---保存退出	
####命令模式（Command mode）
用户刚刚启用vim就进入了命令模式。用户敲击键盘被认为是命令，而不是输入字符  
**vi 文件名 vi后面必须加文件名，不管文件存在与否**  

* i （insert）切换到插入模式(i/o/a都可以进入编辑模式)
* x 删除当前光标所在处的字符
* ：切换到底线命令模式，以在最低一行输入命令

####输入模式（Insert mode）

* esc  退出输入模式，切换到命令模式

####底线命令模式（Last line mode）
在命令模式下按下：（英文冒号）就进入底线命令模式  
底线命令模式可以输入命令 
 
* :q 退出程序 ，没有改动时
* :q! 退出程序，且不保存 
* :w 保存文件
* :wq  推出且保存
按esc可以退出底线模式

###vi／vim按键说明  
####第一部分：一般模式下，可用的光标移动、复制粘贴、搜索替换 
一般模式下。即推出编辑模式状态下
####光标移动（常用） 
 
* h、j、k、l 表示光标向左、下、右、上移动
* ctrl+f 向下翻页 page down
* ctrl+b 向上翻页
* n<space> n代表数字，输入数字再空格。光标向后移动n个字符
* 0 表示光标移到这一行的第一位
* ¥（英文下的）表示光标移到这一行的最后
* G 移动到该文档的最后一行
* gg 移动到这个文档的第一行
* n<Enter> 光标向下移动n行

####搜索替换
* ／word 向光标下搜索word这个字符串 
* ？word 向光标上搜索word这个字符串
* n （英文按键）代表重复前一个搜索动作。如果执行的是／world ，则会向下一直搜索；如果执行？world，则会向上一直搜索
* N （英文按键）与n相反，重复前一个动作反向搜索。如果前面执行了／world，则会向上搜索
* :n1,n2s/word1/word2/g  n1和n2是数字。在第n1行到n2行内搜索word1，并将其替换成word2 （常用）
* :n1,¥s/word1/word2/g （¥应该是英文状态下的）从第一行到最后一行搜索word1，并将该字符替换为word2
* :n1,¥s/word1/word2/gc 替换前显示给用户确认（confirm）是否替代

####删除、复制、黏贴

* nx/X 向后／前 删除n个字符 如10x／X分别表示向后／前删除10个字符
* ndd 向下删除n行(包括光标所在行)
* yy 复制光标所在的那行
* nyy 复制光标所在的向下n行
* p/P 将复制的内容，在光标的下一行／上一行贴上
* u 复原上一个动作。即回退上一个动作
* . 点表示重复上一个动作  

####vim的环境变量  
* ：set nu 输入模式显示行号(行号不会被保存在文档中)
* ：set nonu 取消行号显示
##Linux yum命令
yum（Yellow dog Updater,Modefied）是一个在Fedora和RedHat、SUSE中的Shell前端软件包管理器。                
yum 语法：yum [options] [command] [package]

* options：可选。包括-h (help)、-y（当安装过程提示选择都选yes）、-q（不显示安装过程）
* command：要进行的操作
* package：操作的对象
###yum 常用命令 
* yum check-update ：列出所有可更新的软件
* yum update：更新所有软件
* yum install <package_name>：仅安装指定的软件
* yum list：列出所有可安装的软件
* yum remove <package_name>：删除指定软件
* yum search <keyword>：查找软件包
* 清除缓存：
 * yum clean packages：清楚缓存目录下的软件包
 * yum clean headers：清楚缓存目录下的headers
 * yum clean oldheaders：清楚缓存目录下旧的headers
 * yum clean，yum clean all（=yum clean packages；yum clean oldheader）：清楚缓存目录下的软件包及旧的headers  
安装软件实例：  
 yum install pam-devel  
删除软件实例：  
 yum remove pam-devel  




 






       
          
 
  
 






