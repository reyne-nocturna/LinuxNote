# linuxNote_@Rey (lessons of MicroFrank)

[toc]

# Basic Shell Commands(bash)

## Shell命令的开始/linux文件系统粗解

### 命令参数

- 最常用的指令：


​		`ll`

- 清除：


​		`clear or ctrl + l` 

- manual page:


​		`man`

​		如 `man ls`

```bash
$ ls
$ ls -l
$ ll
$ ls -hl # 可读大小
$ ls -al # 所有文件包括隐藏
```

wangchujiang.com/linux-command Linux命令查询网站

`exit # 退出`

### linux根目录root dir及文件系统filesystem

- win VS linux

  - win:盘符；G:\Game\TencentGame\LOL...反斜线
  - linux: 全是文件 /usr/... 正斜线

- ~ 用户home目录

- `cd` 切换目录

- /$ ... /为根目录

- /bin 二进制目录 GNU工具 ls等自带命令

  - 存放许多用户级；系统命令

- /etc **系统配置文件目录**

   //window里注册表编辑器；windows文件夹中是配置文件；

- /home 主目录，显示所有用户目录；

- /lib 库目录   如软件A需要B,B就在lib里；eg.使用lol一键写符文 。-->wegame---lol

- /lib64

- /lost+found ...断电 突发

- /mnt 挂载目录

  ​	如，U盘.. 挂载--外在设备与电脑连接

- /proc 伪文件目录 虚拟文件系统

  ​	（新手不用理解

- /run 运行目录（临时，也可能不删除

- /snap ubuntu的产物，沙盒什么的（不用理解

- /tmp 临时目录（temp

- /var 可变目录 log等经常变化的文件

- /boot 启动目录，启动时的操作，慎用

- /dev 设备目录 创建设备节点

  ​	如win点管理，设备管理器里的 驱动程序 web端口等 就是设备目录

  ​	linux里的硬件设备相关在设备目录里

- /media 媒体目录

- /opt 可选目录；第三方软件包

- /root 管理员身份

  - root用户的主目录，高级权限

  - /$ su
  - rm -f
  - sudo rm -rf 删库命令

- /sbin 系统二进制目录，GNU高级管理员使用的命令工具
- /srv 服务目录 本地服务
- /usr 用户二进制目录，GNU工具
  - /usr/bin 自己安装的软件 gcc，python等

- > FHS 文件系统层级标准 Filesystem Hierarchy Standard

  - 介个文件就是最全的了

## cd

`cd /home/rey`

`cd ~` 即可进入用户目录

`cd` 即可默认change dir到用户目录

`cd .`当前目录 `cd ..`上级目录

<span style="color:">cd到dir 后可接 绝对路径or相对路径</span>

```bash
cd !$ # 把上个命令的参数作为cd参数使用
pwd # print working dir
```

## ctrl c

```bash
^c # 输入命令过程中强制退出
ctrl shift c/v # linux中复制粘贴
# mac-OS 上是 command(win位那个键) c/v
```

linux的终端是无法撤销的；编写时可以撤销，不是`ctrl z`

## 路径 relative/absolute path

相对：相对于谁？

Home/Documents/doc/1.txt

```bash
rey@nightcity:~$ gedit /home/rey/Documents/doc/1.txt # 绝对路径
# 绝对路径可在任何地方打开
```

```bash
rey@nightcity:~$ gedit Documents/doc/1.txt # 相对路径
```

```bash
rey@nightcity:~$ gedit /Documents/doc/1.txt # linux会觉得/是根目录！并创建临时文件夹即 *1.txt 但系统目录无法操作 所以没有创建Documents等；所以别加/
```

```bash
rey@nightcity:~$ gedit ./Documents/doc/1.txt # 要么不加，要么加./
```

## 命令进阶

参数

```shell
rey@nightcity:~$ ls Documents/ -F -R # -F 每个目录名加“/”后缀；每个FIFO加“|”后缀，可运行加“*”后缀；
Documents/:
doc/ pdf/
rey@nightcity:~$ ls Documents/ -FRSA # 多flag组合
# 上下键切换历史命令
rey@nightcity:~$ ls -laR
rey@nightcity:~$ ls -laF # 常用，小写放前面
```

### 查找文件

文件名过滤：`ls -l 文件名`

**文件扩展匹配符**：`*` 多个符号 `?` 一个占位符号

```bash
rey@nightcity:~/Documents/pdf$ ls
fhs-2.3_copy1.pdf fhs-2.3_copy2.pdf fhs-2.3.pdf
rey@nightcity:~/Documents/pdf$ ls -l fhs-2.3_copy?.pdf
-rwxrw-rw- 1 rey rey 510762 Jan 3 11:36 fhs-2.3_copy1.pdf
-rwxrw-rw- 1 rey rey 510762 Jan 3 11:36 fhs-2.3_copy2.pdf
rey@nightcity:~/Documents/pdf$ ls -l fhs-2.3_*.pdf
-rwxrw-rw- 1 rey rey 510762 Jan 3 11:36 fhs-2.3_copy1.pdf
-rwxrw-rw- 1 rey rey 510762 Jan 3 11:36 fhs-2.3_copy2.pdf
```

`ls -l *.扩展名`

```bash
rey@nightcity:~/Documents/pdf$ ls
1.txt fhs-2.3_copy1.pdf fhs-2.3_copy2.pdf fhs-2.3.pdf
rey@nightcity:~/Documents/pdf$ ls -l *.pdf
-rwxrw-rw- 1 rey rey 510762 Jan 3 11:36 fhs-2.3_copy1.pdf
-rwxrw-rw- 1 rey rey 510762 Jan 3 11:36 fhs-2.3_copy2.pdf
-rwxrw-rw- 1 rey rey 510762 Jan 3 11:36 fhs-2.3.pdf
```

### 元字符通配符

`ls -l f[a-x]ck.txt`

## touch

touch不会覆盖文件内容；同名文件只会更新时间；若无会创建

```
touch 1.txt 2.txt
ls
1.txt 2.txt
```

## cp

可复制文件or文件夹；若无会创建

`cp 源文件 目标文件` 

`cp 具体文件 `

`cp 路径 路径`

`cp 路径 文件`  eg.   `cp ../pdf/* .`

**会覆盖文件内容！**危险捏

`cp -i` 覆盖前询问  **强制要求 `-i` 哦**

ctrl+c 用于取消 copy `cp: overwrite '2.txt  '? ^C` or `y `: yes

`cp -r` 复制文件下的内容，**连同文件夹本身** 

`cp 文件夹/*`只会复制文件夹下内容

### cp -r 练习

```bash
rey@nightcity:~/Project$ ls
touch 1.java 2.java 3.java 4.mp3 5.mp4 6.java
rey@nightcity:~/Project$ pwd
/home/rey/Project
rey@nightcity:~/Project$ cp -r ./*.java ~/Documents/temp/
rey@nightcity:~/Project$ cd ~/Documents/temp/
rey@nightcity:~/Documents/temp$ ls
1.java 2.java 3.java 6.java
```

小tip：`cd -` 返回到上一个目录

## 终端光标移动技巧

很多子目录无法-r find命令

制表符 `tab` 键 自动补全

`ctrl +` 左右方向键跳单词编辑（下划线切割） `rm create_file_temp_jjjPkdjfidfds.c`

`ctrl + A` 跳到整个命令的开头

`ctrl + E` 跳到结尾

`ctrl + B` 往前移动 ctrl + F 往后移 字母

`ctrl + H` 删除 相当于退格键

`ctrl + T` 往后挪某个字母

`ctrl + u` 删除整行（光标之前的东西）

`ctrl + K` 删除光标之后的东西

`ctrl + R` 搜索之前用过的命令

`ctrl + P ctrl + N` 上一个命令 下一个命令 同上下键

`ctrl + J` 回车

## lnk链接文件

windows中： .lnk (link files) 快捷方式

linux: 链接文件

1. 符号链接/软链接 [symbolic links/soft links] (快捷方式) 
   * 原文件（夹）必须存在
2. 硬链接 [hard link] 
   * 可理解为创建副本
   * 原文件（夹）必须存在
   * `geek.exe`   `geek-副本(2).exe`    `geek-副本(3).exe` windows上修改原文件，副本不变；但Linux上不是！

## move

### `mv` move(rename) files 移动/重命名

```bash
rey@nightcity:~/Project$ mv test.c ~/Documents/pdf/
rey@nightcity:cd !$
cd ~/Documents/pdf/
rey@nightcity:~/Documents/pdf$ ls
fack.txt fbck.txt fuck.txt fxck.txt fzck.txt test.c
```

`cd !$` 转到上一个命令后路径的最后的文件位置

### `rm` 删除 remove

```shell
rey@nightcity:~/Documents/pdf$ sudo rm -rf /* # 很危险的命令！！
# 后面可以用github第三方回收站替代rm
# rm 一定要加 -i
```

`rm` 永久、彻底删除  没有回收站

`rm -rf`  f: 强制删除  `rm -r`  to remove a directory # r: recursively

`rm -i` 询问是否删除

所谓的"删库跑路"

## Create and Delete dir

directory 目录（文件夹）

`mkdir` make directory

```bash
rey@NC:~/Project$ mkdir java
rey@NC:~/Project$ ls
java
```

`mkdir -p js/src/util # -p: parent dir`

`rmdir` remove empty dir 没什么用 还得是 `rm -i` `rm -rf # not recommended`

## 查看文件&文件类型

`file` 探测给定文件的类型

```bash
rey@NC:~/Project$ file 1.txt
1.txt: ASCII text
rey@NC:~$ file Project/
Project/: directory
```

## cat ,more, less查看(打开)文件 

### cat

```bash
rey@NC:~/Project/java$ cat 1.java
rey@NC:~/Project/java$ cat 2.txt
asdfjiowjdfcs
# 适合查看短的东西
rey@NC:~$ cat 444
444
rey@NC:~$ file 444
444: ASCII text
cat -A 2.txt # $的符号替代回车
cat -n 2.txt # 显示行号
```

### more

`more`  按页展示；使用前清屏；下端显示百分比（用途也不大）

`b` last page `space ` next page  `enter` next line `q` quit

### less

分屏上下页浏览；允许向前or向后（more只能向后）浏览文件

`PageUp # 向上翻页`  `PageDown # 向下翻页` `q # quit`

键盘上 `Home # 1st page` `End # last page`

```bash
-f: 强制显示文件
-g: 不加亮显示所有关键词；仅显示当前关键字
-l: 忽略大小写
-N: 行号
-s: 压缩空行
-S: 单行显示
-x<num>: tab->指定num的<space>
```

`/fd 回车 # 搜索fd`

但是也不怎么用（乐

## tail, head

`tail # 指定文件的末尾若干行 比如log文件`

`tail demo.c # last 10 lines`

`tail -n 2 demo.c # last 2 lines` 

`head # 开头`

# upToSystem(more bash shell)

## 任务管理器task manager

windows：进程...服务service 检测需求

linux:

* System Monitor
  * Processes
  * Resources
  * File Systems

用命令实现任务管理器的查看

`top` 实时动态查看系统整体运行情况；用热键可以管理

​	pageup/down翻页 `q` 退出

`ps` 报告系统进程状态 process status ` PID TTY TIME CMD # 在终端里干了什么)` 

* **`man ps` 超复杂**
* `ps axo pid,comm,pcpu`查看PID(类似身份证 病号)；名称(进程名称)；CPU占用率
* `ps -aux | grep named # 查看named进程详细信息` **常用**
* 只要进程相关，ps命令就可能有用哦！比如做运维

## kill

```bash
ps -aucx | grep gedit
# get pid of gedit
kill 2974 # 2974:pid 对应进程终结
```

`kill -9 # 暴力杀杀`

**还有很多自己去学。**

## 挂载mounting

比如插入u盘，电脑生成虚拟的盘：创建一个临时的盘供用户使用就叫做挂载。

linux中，真正的目录在：`/media/rey/USB`

### 改变挂载的目录/路径

windows 

 * 磁盘管理 更改驱动号和路径（挂载点）但不安全

linux

* `/media/rey/VMware Tools`

* ```bash
  cd /
  cd mnt/
  sudo mkdir KingUSB
  mkdir: cannot... # 自动挂载点 不允许写入
  mount
  sudo fdisk -l # 显示真实路径 Device: /dev/sdc1（设备的根目录，无法访问）
  # 默认挂载到medie
  # 尝试改变映射路径：sudo mount 真实路径 目标路径
  sudo mount /dev/sdc1 /mnt
  cd rey/
  ls
  USB
  ls
  cd mnt/
  ls
  # 同时，mnt也挂载了USB里的东西
  sudo umount /mnt/ # 卸载，而media中不受影响
  umount /media/frank/USB # 正在使用无法卸载 加sudo也不行；
  # 注意不是unmount
  cd ..
  # 退出USB就可以卸载了 
  ```

### 为什么要有挂载

现在：自动挂载；没弹出u盘or`dev -h` 没有u盘 可能需要手动挂载；还有权限问题

### 安卓挂载

```bash
cd /media/
ls
rey
cd rey/
ls
cd mnt/
ls
cd ..
ls
cd run/
ls
cd user
ls
cd 1000
ls
cd gvfs/
ls
'mtp:host=Google_Poxel_2_XL_910KPGS2081839' # 手机型号
cd mtp
ls
cd 内部共享存储空间
sudo mount /run/user/1000/gvfs/mnt
# mtp协议，不行，挂载的得是一个分区，不能是绝对路径（把一个分区挂载到一个目录上，而不能把目录挂载到目录）
# 可以用abd
```

## df du

`df # 查看磁盘空间 `

`Filesystem 1K-blocks Used Available Use% Mounted on`

`df -h` 简洁

`du # 当前目录；特定目录磁盘使用情况，判断啥玩意用的空间最多，作用貌似不大`

`du -h # 常用，查看文件夹使用情况 `

## sort文件排序

`sort` 对文本文件排序；不改变源文件

常用：

```bash
sort -M # Jan, Feb...在日志中，方便排序；  
gedit time.log
sort -M time.log
sort -Mr # 倒序
```

```bash
-b, --ignore-leading-blanks    忽略开头的空白。
-d, --dictionary-order         仅考虑空白、字母、数字。
-f, --ignore-case              将小写字母作为大写字母考虑。
-g, --general-numeric-sort     根据数字排序。
-i, --ignore-nonprinting       排除不可打印字符。
-M, --month-sort               按照非月份、一月、十二月的顺序排序。
-h, --human-numeric-sort       根据存储容量排序(注意使用大写字母，例如：2K 1G)。
-n, --numeric-sort             根据数字排序。
-R, --random-sort              随机排序，但分组相同的行。
--random-source=FILE           从FILE中获取随机长度的字节。
-r, --reverse                  将结果倒序排列。
--sort=WORD                    根据WORD排序，其中: general-numeric 等价于 -g，human-numeric 等价于 -h，month 等价于 -M，numeric 等价于 -n，random 等价于 -R，version 等价于 -V。
-V, --version-sort             文本中(版本)数字的自然排序。
```

```bash
cd /etc/password
# 密码文件
```

```bash
du -sh * | sort -nr
# 排序呈现；每个文件夹的总计大小；两个命令合并显示
```

## 初步了解grep

```bash
grep Hello ./Project/java/demo.c
# 含Hello的标红显示
grep demo.c # 相对路径也可以哦
man grep # 贼拉长，就像ps
```

后面要用到**正则表达式**，蛮复杂的！55

`fgrep `

## 打包压缩归档解压缩

### 压缩工具

windows：

​	windows: winRAR

​	bandizip (韩

​	7-zip

linux:

​	`gzip # 解zip的包`

​	`gzip: .gz` `zip: .zip` `bzip2: .bz2`

### tar

tar打包：一堆文件->一坨总文件

zip压缩：大文件->小文件

`linux 中只能针对一个文件（夹）进行压缩，不能压缩整个文件夹，所以先tar成一个文件，再压缩：`

 `.tar.gz`

```bash
tar -cvf log.tar log2020.log # just tar!
tar -zcvf log.tar.gz log2020.log # tar and gzip 
tar -jcvf log.tar.bz2 log2020.log # tar and bzip2
```

`tar -c # 创建一个新归档`

`tar -f # 使用归档名字，最后一个参数，后接档案名！`

`tar -zcvf` **最常见**

`zcxf # x --extract, --get 解压`

## server上安装vmwartools的方式

```bash
df
sudo mount /dev/sr0 /mnt/ #其实没有必要
df
cd /mnt/
cp VMwar....tar.gz ./home/rey/Desktop/
cd Desktop/
ls
tar -zxvf VMare...tar.gz
cd vmare-tools-distrib/
ls
sudo ./vmware-install.pl
cd Desktop/
rm -ri vmware-tools-distrib/ VMawreTools...tar.gz
yyyyy
或者-rf
sudo umount /mnt && umount /media/rey/VMare ## 装逼
exit
```

# parent-child shell

## concept

bash是shell上其中一个常用软件；还有：dash, tcsh...

```bash
ps
有一个bash
bash
ps -f
有两个bash PPID就是基于谁/上一级
exit
exit
```

## 分号在命令里的作用

```bash
ls ; pwd ; cd / 
依次执行多个命令
(ls ; pwd ; cd /)
加括号：结果一样，但是前者是进程列表，没有生成child shell执行
带了括号会创建child shell 再执行
```

```bash
ls; pwd ; cd / ; echo $BASH_SUBSHELL
...
/
0
(ls; pwd ; cd / ; echo $BASH_SUBSHELL)
...
/
1 # a child shell
```

## sleep, jobs

```bash
$ sleep 10
$ man sleep # delay for a specified amount of time. 延迟or后台执行 单位秒
$ sleep 300& # 挂在后台
[1] 56391 # pid
$ ps -f
```

```bash
$ jobs
[1]+ Running              sleep 300 &
$ sleep 3&
[2] ...
$ jobs -l
[2]+ ... Done             Sleep 3
```

## 后台用法的举例

```bash
$ (tar -zxvf ...; tar -zxvf ..; cp ....)&
放在后台自己解压
```

## coproc

```bash
$ coproc rey { sleep 10; } # 要有空格和分号哦！
[1] 57892
$ jobs
[1] + Running             coproc rey { sleep 10; } 
# 创建child shell; 在其中挂载
$ coproc rey {sleep 10; sleep 3; } &
# 协程
$ jobs
[1]+ Done                 coproc rey {sleep 10; sleep 3; }
```



## 外部命令和内建命令

有的命令单独创建一个进程（如任务管理器;cmd(win);ps(shell)）；

有的命令不占进程（如cd(shell);如dir(win)）

shell中 执行`ps -f` 时；在**上帝视角**（外部）更能看清所有进程（即在 shell外，且依赖bash）

```bash
forking 衍生 # 单独创建一个进程；
```

**外部命令** 如 ` ps -f`

**非外部命令** 或者“内建命令”(built-in) 如`cd` 

如何判断？`type`

```bash
$ type ps
ps is hashed (/usr/bin/ps)
$ type cd 
cd is a shell builtin
$ type cat
cat is /usr/bin/cat
$ type echo
echo is a shell builtin
```

## alias别名

`history # 查看之前运行过的命令,builtin`

`!! # 执行上一个命令`

`$ !1320 # 执行历史中这一行的命令`

```bash
$ alias -p
...
alias ls='ls --color=auto' # ls就是自动高亮
# 可自己创建缩写、别名
$ alias li='ls -li'
$li
# 执行了ls -li
# 只能在当前进程使用；后面再学永久修改，自定义
```

# 环境变量

## 环境变量是啥

environment variables

* user variables
* system variables

```powershell
C:\Users\1>notepad
C:\Users\1>E:
E:\>notepad
## windows中写入Windows(C:)\Windows\System32中的文件，在任何目录都能访问
环境变量中配置了，在任何地方都能访问
（提前预约，最好服务~）
```

## 全局变量，局部变量

win 注销之后，原来的用户的变量就用不了了；系统变量还是能用（可以这么理解）

linux中也是：

* 全局变量（如ls、cd；查看：`printenv`）(相当于win系统变量)；ubuntu和其他的linux系统的可能不一样哦；命令是一样的\

  ```bash
  $ printenv
  ...
  PWD=/home/rey
  HOME=/home/rey
  $ printenv USER
  rey
  $ printenv HOME
  /home/rey
  $ echo $HOME
  /home/rey
  $ echo $PATH
  /usr/local/sbin:/usr/sbin:/usr/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
  # 相当于windows的PATH  改错会出问题！
  $ cd $HOME
  ~$
  ```

* 局部变量（相当于win的局部变量）

```bash
$ set
# 一堆东西啥也看不懂
# 局部的也没啥用捏
```

## 用户和局部变量的设定

！定义用户变量、局部变量用小写：单词间下划线隔开`fuck_you`

在prt定义的局部变量，child bash里不能使用。

## 定义全局变量

### 大写

```bash
$ export fuck="QNMB"
$ echo $fuck
QNMB
$ bash
$ echo $fuck
QNMB
# 可以在child shell里使用
```

### 如何删除

```bash
unset fuck
echo $fuck
# 已删除，在child shell里删除全局变量，只会对child shell有效。
不影响 parent shell里的全局变量
```

## 修改环境变量

### 追加环境变量

```bash
$ PATH=$PATH:/home/rey/Project/
$ echo $PATH
# 就会增加这个path
装到这个路径的软件就会直接执行
坏处：删掉shell就又没力，不是永久配置
```

### 永久配置

linux一切皆文件！启动文件：开机时默认执行环境变量

```bash
$ cat /etc/profile # 启动时候最主要的文件
$ cd /etc/profile.d/
$ ls # 了解即可
$ cat .bashrc # ubuntu配置找这个即可；其他可能是~/.bash_profile ~/.profile ~/.bah_login
# .隐藏文件前面有个点
```

修改后面再讲

# 安装软件

## PMS和软件安装的介绍

package management system **PMS** 包管理系统 `作用：软件安装 更新 卸载`

工具依赖：~~比如装个英雄联盟必须装个wegame（不是~~ 比如qq空间得要qq

PMS:`dpkg` (Debian

dpkg: apt-get, apt-cache, aptitude（最后这个没维护别用惹；基本使用apt） # 解决工具依赖问题；介入第三方工具

`# 高级打包工具 Advanced Packaging Tools **APT** Debian及其派生的Linux软件包管理器；可以自动下载，配置，安装二进制或者源代码格式的软件包 APT构建于dpkg之上` 

```bash
$ sudo apt install vim
```

一些有趣的命令 `$ sudo apt install sl # 小火车` `cmatrix乱码雨` `oneko修猫咪`

## 安装 更新 卸载

 ```bash
 $ apt -h # help
 $ apt list
 $ apt update # 查找更新
 $ apt upgrade # 一键更新
 sudo apt update # 更新整个软件
 sudo apt uprade # 更新当前的系统和软件
 $ sudo apt remove oneko # 卸载
 $ sudo apt remove sl
 ```

## 其他发行版

```bash
ubuntu 20.04 配置镜像源
编辑/etc/apt/sources.list文件
$ cd /etc/apt
$ ls
$ less sources.list
```

```bash
red hat
yum 最常用 help,list...
yum instal xxxx
urpm zyp
```

## 安装第三方软件

 ```bash
 有的软件得看帮助文档才能安装
 比如thefuck
 # 输错了就fuck，再给出提示，爽就完事
 ```

先看README.md

Requirements依赖

然后Installation

比如

```bash
$ brew install thefuck # 苹果电脑OS X的Homebrew(就是一个PMS)特别牛（Linuxbrew on Linux)
如果是ubuntu：
$ sudo apt update
$ sudo apt install python3-dev python3-pip python3-setuptools
$ sudo pip3 install thefuck
# 如果pip卡就再后面加上-i参数指定pip源
pip install xxx -i https://pypi/tuna.tsinghua.edu.cn/simple
```

配置

```bash
 操作步骤：
 先 ctrl shift c 拷贝 eval "$(thefuck --alias)"
$ vim（或者vi） ~/.bashrc
 翻到最后一页 按j 按o跳下一行
 ctr shift v
 按esc
 ：wq
 最后
$ source ~/.bashrc
```

```bash
$ sudo aptgt inssall vim
$ fuck 
上下键，回车
```

**步骤总结**

1. 看软件的使用说明README（软件是干啥的）
2. 看软件依赖Requirements
3. 看软件操作系统、安装方式
4. 如何维护、更新、使用

# 用户和权限

## 含义和作用

id（用以跟踪谁在操作文件，打开程序）

用户id：UID （数字）

```bash
cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
# 不要用root登录，也不要“裸奔”（所有用户给root权限，被黑了就寄）
... 
# 中间的用户是系统账户；有的软件服务需要单独的账户
rey1:x:1001:1001::/home/rey1/t1:/bin/sh
```

1. 用户名；
2. 密码`x` (加密)
3. `系统账户`uid标号<500; `普通账户`标号>500; 
4. 组ID（GID）
5. 用户描述/备注字段
6. 用户home目录
7. 用户默认使用的shell

密码在哪？

```bash
sudo cat /etc/shadow
...
rey:... # 加密的
```

后面的数字：多久前创的密码，多少之后能修改密码，多少天之后必须改密码，过期了提前多少天提醒用户更改密码，过期后多久禁用，禁用日期。。。

## 创建用户，删除，更改

`useradd` 添加新用户

 `	userdel `  删除

```bash
sudo useradd rey2
sudo userdel rey2
```

`usermod` 修改passwd的字段

```bash
sudo passwd rey2 # sudo才能用
chpasswd # 从txt文件中读取
sudo chpasswd < passwd.txt # user1:12345 user2:45678
```

*TODO: `chsh` `chfn` `chage` 自己去研究这些*

chage E # 设置expire date过期日期

## group组

组的目的：共享资源（共用权限）——控制有的组能用，有的不能

但是：linux不同发行版略有差异；有的发行版把所有用户纳入一个组（达咩哦）；有的发行版给每个用户单独创个组(与账户同名)，比如ubuntu // ubuntu不允许所有用户同个组

```bash
tail /etc/group
组名：组密码：组id（GID）：（属于该组的列表）
# 不要通过改group文件获取权限
要用usermod把用户添加到组里，最好先创一个
sudo groupadd reygroup # 创建组
groupmod # 修改组
groupdel # 删除组
```

## File Permissions文件和文件夹权限

```bash
-rw-r--r-- 12 linuxize users 12.0K Apr  28 10:10 file_name
|[-][-][-]-   [------] [---]
| |  |  | |      |       |
| |  |  | |      |       +-----------> 7. Group
| |  |  | |      +-------------------> 6. Owner
| |  |  | +--------------------------> 5. Alternate Access Method
| |  |  +----------------------------> 4. Others Permissions # 其他帮派成员
| |  +-------------------------------> 3. Group Permissions # "帮派"下属成员
| +----------------------------------> 2. Owner Permissions #"帮派"创始人
+------------------------------------> 1. File Type # -文件，d目录
```

## chmod修改权限（自学）

`chmod ugo+r file1.txt` # user group other

`chmod a+r *`

`chmod u=rw, go= file`

`chmod 777`

# vim

## 配置

`vim .vimrc`

```bash
set syntax=on # highlight
set tabstop=4
set softtabstop=4
set number # 显示行号
set enc=utf-8
set showmatch # 括号匹配
```

`source .vimrc`

`行号+gg` 跳跃

## 简单使用

esc

i (insert)

:wq

## 移动

hjkl

## 翻页

ctrl f （下）

ctrl b （上）

G 末尾

gg 开头

## 编辑 跳跃

i 插入光标的前面

a 光标后面插入

o 跨行插入（enter）

x 删除光标所在

dd 删除行

u 撤销

dw 删除光标后单词

b 跳跃上一个单词首字母

e 跳跃单词屁股

w 跳跃下一个单词首字母

w b e + shift 大跳

## 跳跃行首行尾

shift+6：^ 跳跃到本行开头

shift+4： $ 跳跃本行末尾

**普通模式下别用退格backspace**

## 大括号跳跃函数段落

{}

## 复制粘贴

y,p

yw 复制一个单词

y$ 当前复制到行末尾

p粘贴

## Visual 可视化模式

v

V按行选中

全删：gg v G d

o跳跃选中首尾

0补全角落；

v a w 快速选中单词

vab小括号内容

vaB包含大括号

va<包含尖括号，删除

## v其他操作

v shift <> 缩进

v ~大小写转换

v U变大写

v u变小写

## 查找和替换

`/`要查找的东西 回车 定位

下一个：按`n`跳跃

替换 输入`:s/要替换的东西/换成的东西/g`（g：一行全换）（命令模式）

替换全部？`:%s/old/new/g`

临时显示行号`:set number`

修改部分行的内容 `:开始行,结束行,s/old/new/g` (中间取值)

带有提示的`:%s/old/new/gc` (c:comment,y？)



