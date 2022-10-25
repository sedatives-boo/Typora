# Ubuntu 安装和分区

- 先下载该系列教程（提取码：8qfg）：https://pan.baidu.com/s/1EHsgLsUZGOBzwNcEuDUKWA



- 找到如图箭头目录上的两个视频，并看完，你对 Ubuntu 的安装就有了一个大概的了解，视频中 Ubuntu 虽然版本较早 13.04 的， 但是没关系，对于 Ubuntu 来讲新旧版本安装基本都一样的，所以别担心，驱动的问题也别担心，我们不是要在 Ubuntu 打游戏的，所以常见驱动系统是已经帮我们集成的不会影响使用。但是分区这一块的话，我个人建议是手工分区，视频中没有最终执行手动分区，只是演示了一下又返回了。 我个人是要求你手动分区的。

- 但是再讲分区之前，用什么设备安装是第一前提，我这里推荐用 U 盘，你准备一个 4 G 以上的 U 盘，把 Ubuntu 系统进行格式化到里面，用这个 U 盘作为安装盘进行安装。这个过程不难，具体看如下文章：

- [http://www.Ubuntukylin.com/ask/index.php?qa=jc_1](http://www.ubuntukylin.com/ask/index.php?qa=jc_1)

- http://www.wubantu.com/36bc2075036fab76.html

- http://tieba.baidu.com/p/2795415868

- [http://www.Ubuntukylin.com/public/pdf/UK1410install.pdf](http://www.ubuntukylin.com/public/pdf/UK1410install.pdf)

- 好了假设你现在已经格式化好 U 盘，现在可以开始讲分区了。这里特别说明的是有多个硬盘的，多块硬盘分区方案就没视频中那么简单，特别是 Linux 的盘符不了解的就更加难了，所以看下图：

  

- 以我这边为例：我这边机子的硬盘是：一个 128 G 固态 + 500 G 的机械，我给一个分区方案给你们参考。下面的内容需要你先看过视频才能看懂：
- Linux 一般可分 3 个分区，分别是 `boot 分区`、`swap 分区` 和 `根分区`（根分区也就是斜杠/） boot 是主分区类型，swap 是是逻辑分区，/ 是逻辑分区，其他如果你还想划分的也都是逻辑分区。 最近年代生产的的主板，可能还需要分出一个 EFI 分区启动。EFI 的选择和 swap 一样，都在那个下拉菜单中。 怎么判断你要不要分出一个 EFI 呢？如果你根据我的要求分了 boot，swap，根之后，点击下一步报错，有提示 EFI 相关的错误信息，那就分一个给它，我这边就是有报错的。
- **120 G 固态硬盘：**
  - `/boot` == 1G（主分区），这里为boot单独挂载是有必要的。系统崩溃的时候，损坏的是这个分区。我们重装系统之后，其他分区我们保留下来，重新挂载上去就可以用了。
  - `/EFI` == 100M（主分区）（我有提示报错需要分这个，我就分了）
  - `/swap` == 12G（逻辑分区）一般大家的说法这个大小是跟你机子的内存大小相关的，也有说法内存大不需要这个，但是还是建议分，我内存是12G，所以我分12G。
  - `/` == 100G（逻辑分区）
- **500 G 机械硬盘：**
  - `/home` == 500G（逻辑分区）
- 分区后的安装都是下一步的，而且 Ubuntu kylin 还是中文的说明，所以没啥难度。 到此假设你给自己的电脑安装了 Ubuntu，那下一讲我将讲 Ubuntu 的相关设置。
- 如果你想用 VMware 虚拟机安装，这个教程推荐给你，讲得很详细。
  - http://www.jikexueyuan.com/course/1583.html

- [Ubuntu 网络相关设置问题](https://github.com/sedatives-boo/Linux-Tutorial/blob/master/markdown-file/ubuntu-settings/Network-Settings.md)
- [Ubuntu 源设置](https://github.com/sedatives-boo/Linux-Tutorial/blob/master/markdown-file/ubuntu-settings/Ubuntu-Extra-Packages.md)
- [Ubuntu 给 Dash 添加程序图标](https://github.com/sedatives-boo/Linux-Tutorial/blob/master/markdown-file/ubuntu-settings/Ubuntu-Create-Desktop.md)
- [Ubuntu 常用设置](https://github.com/sedatives-boo/Linux-Tutorial/blob/master/markdown-file/ubuntu-settings/Ubuntu-Popular-Settings.md)
- [Ubuntu 常见桌面环境方案](https://github.com/sedatives-boo/Linux-Tutorial/blob/master/markdown-file/ubuntu-settings/Ubuntu-UI.md)

# Ubuntu 安装 VMware

- 我个人习惯使用 VMware，在一些个性化和兼容性上，我觉得 VMware 比 box 好很多

## 安装说明

- 下载：VMware-Workstation-Full-10.0.4-2249910.x86_64.bundle
  - 下载地址（rzb0）：http://pan.baidu.com/s/1dFuLD2D
- 安装组件：

```
命令：sudo apt-get update
命令：sudo apt-get install build-essential linux-headers-`uname -r`
```

- 进入软件下载后目录，比如我在 /opt/setups 下
  - `cd /opt/setups`
  - `chmod +x VMware*.bundle`
  - `sudo ./VMware*.bundle`
- 接下来会弹出图形界面，则效果跟 Windows 一样，那就没啥好说了。

## 资料

- [How To Install VMware Workstation 11 On Ubuntu 14.10](https://www.liberiangeek.net/2014/12/install-vmware-workstation-11-ubuntu-14-10/)

# Vim 安装和配置、优化

## Vim 介绍

- Vim 官网：http://www.vim.org/

## Vim 安装

- CentOS：`sudo yum install -y vim`
- Ubuntu：`sudo apt-get install -y vim`
- Windows GVim 下载：http://www.xiazaiba.com/html/3347.html

## Vim 配置（CentOS 环境）

- 编辑配置文件是：`sudo vim /etc/vimrc`

## Vim 基础快捷键

- 注意
  - 严格区分字母大小写
  - 含有 `Ctrl` 字眼都表示 Ctrl 键盘按钮
  - 特定符号需要配合 Shift 键，比如字母键盘区上面的数字区：!@#%%^&*()
  - 要按出冒号键 `:` 也是需要 Shift 的
- 移动
  - `j`，下
  - `k`，上
  - `h`，左
  - `l`，右
  - `v`，按 v 之后按方向键可以选中你要选中的文字
  - `gg`，跳到第 1 行
  - `G`，跳到最后一行
  - `16G` 或 `:16`，跳到第 16 行
  - `$`，到本行 **行尾**
  - `0`，到本行 **行头**
  - `w`，到下一个单词的 **开头**
  - `e`，到下一个单词的 **结尾**
  - `Ctrl + u`，向文件 **首翻** 半屏
  - `Ctrl + d`，向文件 **尾翻** 半屏
  - `Ctrl + f`，向文件 **尾翻** 一屏
  - `Ctrl + b`，向文件 **首翻** 一屏
  - `*`，匹配光标当前所在的单词，移动光标到 **下一个** 匹配单词
  - `#`，匹配光标当前所在的单词，移动光标到 **上一个** 匹配单词
  - `^`，到本行第一个单词头
  - `g_`，到本行最后一个单词尾巴
  - `%`，匹配括号移动，包括 **(、{、[**
- 插入
  - `I`，在当前 **行首** 插入
  - `A`，在当前 **行尾** 插入
  - `i`，在当前字符的 **左边** 插入
  - `a`，在当前字符的 **右边** 插入
  - `o`，在当前行 **下面** 插入一个新行
  - `O`，在当前行 **上面** 插入一个新行
- 编辑
  - 删除
    - `x`，删除 **光标后** 的 1 个字符
    - `2x`，删除 **光标后** 的 2 个字符
    - `X`，删除 **光标前** 的 1 个字符
    - `2X`，删除 **光标前** 的 2 个字符
    - `dd`，删除当前行
    - `cc`，删除当前行后进入 insert 模式
    - `dw`，删除当前光标下的单词/空格
    - `d$`，删除光标至 **行尾** 所有字符
    - `dG`，删除光标至 **文件尾** 所有字符
    - `3dd`，从当前光标开始，删掉 3 行
    - `echo > aa.txt`，从 bash 角度清空文件内容，这个比较高效
  - 复制
    - `y`，复制光标所选字符
    - `yw`，复制光标后单词
    - `yy`，复制当前行
    - `4yy`，复制当前行及下面 4 行
    - `y$`，复制光标位置至 **行尾** 的内容
    - `y^`，复制光标位置至 **行首** 的内容
  - 粘贴
    - `p`，将粘贴板中内容复制到 **光标之后**
    - `P`，将粘贴板中内容复制到 **光标之前**
  - 其他
    - `ddp`，交换当前光标所在行和下一行的位置
    - `u`，撤销
    - `:wq`，退出并 **保存**
    - `:q!`，退出并 **不保存**
    - `Ctrl + v`，进入 Vim 列编辑
    - `guu`，把当前行的字母全部转换成 **小写**
    - `gUU`，把当前行的字母全部转换成 **大写**
    - `g~~`，把当前行的字母是大写的转换成小写，是小写的转换成大写
    - `:saveas /opt/setups/text.txt`，另存到 /opt/setups/text.txt
- 搜索
  - `/YouMeek`，从光标开始处向文件尾搜索 YouMeek 字符，按 `n` 继续向下找，按 `N` 继续向上找
  - `?YouMeek`，从光标开始处向文件首搜索 YouMeek 字符，按 `n` 继续向下找，按 `N` 继续向上找
- 替换
  - `:%s/YouMeek/Judasn/g`，把文件中所有 YouMeek 替换为：Judasn
  - `:%s/YouMeek/Judasn/`，把文件中所有行中第一个 YouMeek 替换为：Judasn
  - `:s/YouMeek/Judasn/`，把光标当前行第一个 YouMeek 替换为 Judasn
  - `:s/YouMeek/Judasn/g`，把光标当前行所有 YouMeek 替换为 Judasn
  - `:s#YouMeek/#Judasn/#`，除了使用斜杠作为分隔符之外，还可以使用 # 作为分隔符，此时中间出现的 / 不会作为分隔符，该命令表示：把光标当前行第一个 YouMeek/ 替换为 Judasn/
  - `:10,31s/YouMeek/Judasn/g`，把第 10 行到 31 行之间所有 YouMeek 替换为 Judasn

## Vim 的特殊复制、黏贴

- Vim 提供了 12 个剪贴板，分别是：

  ```
  0,1,2,3,4,5,6,7,8,9,a,"
  ```

  ，默认采用的是

   

  ```
  "
  ```

  ，也就是双引号，可能你初读感觉很奇怪。你可以用 Vim 编辑某个文件，然后输入：

  ```
  :reg
  ```

  。你可以看到如下内容：

  - [![vim](https://github.com/sedatives-boo/Linux-Tutorial/raw/master/images/Vim-Cut-And-Paste-a-1.png)](https://github.com/sedatives-boo/Linux-Tutorial/blob/master/images/Vim-Cut-And-Paste-a-1.png)

- 复制到某个剪切板的命令：`"7y`，表示使用 7 号剪切板。

- 黏贴某个剪切板内容：`"7p`，表示使用 7 号剪切板内容进行黏贴

## Vim 配置

- 我个人本地不使用 Vim 的，基本上都是在操作服务器的时候使用，所以这里推荐这个配置文件
  - [vim-for-server](https://github.com/wklken/vim-for-server)
  - 在假设你已经备份好你的 Vim 配置文件后，使用该配置文件：`curl https://raw.githubusercontent.com/wklken/vim-for-server/master/vimrc > ~/.vimrc`
  - 效果如下：
    - [![vim-for-server](https://raw.githubusercontent.com/wklken/gallery/master/vim/vim-for-server.png)](https://raw.githubusercontent.com/wklken/gallery/master/vim/vim-for-server.png)
- 需要特别注意的是，如果你平时粘贴内容到终端 Vim 出现缩进错乱，一般需要这样做：
  - 进入 vim 后，按 `F5`，然后 `shift + insert` 进行粘贴。这种事就不会错乱了。
  - 原因是：`vim ~/.vimrc` 中有一行这样的设置：`set pastetoggle=<F5>`

## 其他常用命令

- 对两个文件进行对比：`vimdiff /opt/1.txt /opt/2.txt`

## 资料

- [vim几个小技巧（批量替换，列编辑）](http://blogread.cn/it/article/1010?f=sa)
- [最佳vim技巧](http://www.2maomao.com/blog/wp-content/uploads/vim_tips.txt)
- [简明 Vim 练级攻略](http://coolshell.cn/articles/5426.html)
- [vim 批量查找替换](http://blog.csdn.net/wangchong0/article/details/6801956)

# SSH 免密登录

## 环境说明

- CentOS 7.3

## 关键点

- 免密登录的关键点在于理解谁登录谁。
- A 生成的公钥给 B，也给 C、D，则 A 可以直接免密 SSH 登录 B、C、D

## A 生成密钥

- 在 A 机器上输入命令：

  ```
  ssh-keygen
  ```

  - 根据提示回车，共有三次交互提示，都回车即可。

- 生成的密钥目录在：**/root/.ssh**

- 写入：`cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys`

- 测试：`ssh localhost`

## 把 A 的公钥发给 B

- 假设 B 机器的 ip：`192.168.1.105`
- 则在 A 机器上输入：`ssh-copy-id -i /root/.ssh/id_rsa.pub -p 22 root@192.168.1.105`，根据提示输入 B 机器的 root 密码，成功会有相应提示

## 测试 A 免密登录到 B

- 在 A 机器上输入命令：`ssh -p 22 root@192.168.1.105`，则会相应登录成功的提示

------

## 如果是用 pem 登录的话，用 ssh-copy-id 是无法使用的

- 先保存 A 的 pub 到本地：`sz /root/.ssh/id_rsa.pub`

- 登录 B 机子：`cd /root/.ssh/`

- 如果 B 机子没有 authorized_keys 文件则创建：

  ```
  touch /root/.ssh/authorized_keys
  ```

  - 设置权限：`chmod 600 /root/.ssh/authorized_keys`

- 上传 pub 文件到 B 机子，并在 B 机子上执行：`cd /root/.ssh/ && cat id_rsa.pub >> authorized_keys`

# Bash 常用命令

## 基础常用命令

- `某个命令 --h`，对这个命令进行解释

- `某个命令 --help`，解释这个命令(更详细)

- `man某个命令`，文档式解释这个命令(更更详细)(执行该命令后,还可以按/+关键字进行查询结果的搜索)

- `Ctrl + c`，结束命令

- `TAB键`，自动补全命令（按一次自动补全，连续按两次，提示所有以输入开头字母的所有命令）

- `键盘上下键`，输入临近的历史命令

- `history`，查看所有的历史命令

- `Ctrl + r`，进入历史命令的搜索功能模式

- `clear`，清除屏幕里面的所有命令

- `pwd`，显示当前目录路径（常用）

- `firefox&`，最后后面的 **&** 符号，表示使用后台方式打开 Firefox，然后显示该进程的 PID 值

- `jobs`，查看后台运行的程序列表

- `ifconfig`，查看内网 IP 等信息（常用）

- `curl ifconfig.me`，查看外网 IP 信息

- `curl ip.cn`，查看外网 IP 信息

- ```
  locate 搜索关键字
  ```

  ，快速搜索系统文件/文件夹（类似 Windows 上的 everything 索引式搜索）（常用）

  - `updatedb`，配合上面的 locate，给 locate 的索引更新（locate 默认是一天更新一次索引）（常用）

- ```
  date
  ```

  ，查看系统时间（常用）

  - `date -s20080103`，设置日期（常用）
  - `date -s18:24`，设置时间，如果要同时更改 BIOS 时间，再执行 `hwclock --systohc`（常用）

- `cal`，在终端中查看日历，肯定没有农历显示的

- `uptime`，查看系统已经运行了多久，当前有几个用户等信息（常用）

- `cat 文件路名`，显示文件内容（属于打印语句）

- `cat -n 文件名`，显示文件，并每一行内容都编号

- `more 文件名`，用分页的方式查看文件内容（按 space 翻下一页，按 *Ctrl + B* 返回上页）

- ```
  less
  ```

  文件名，用分页的方式查看文件内容（带上下翻页）

  - 按 **j** 向下移动，按 **k** 向上移动
  - 按 **/** 后，输入要查找的字符串内容，可以对文件进行向下查询，如果存在多个结果可以按 **n** 调到下一个结果出
  - 按 **？** 后，输入要查找的字符串内容，可以对文件进行向上查询，如果存在多个结果可以按 **n** 调到下一个结果出

- ```
  shutdown
  ```

  - `shutdown -hnow`，立即关机
  - `shutdown -h+10`，10 分钟后关机
  - `shutdown -h23:30`，23:30 关机
  - `shutdown -rnew`，立即重启

- `poweroff`，立即关机（常用）

- `reboot`，立即重启（常用）

- ```
  zip mytest.zip /opt/test/
  ```

  ，把 /opt 目录下的 test/ 目录进行压缩，压缩成一个名叫 mytest 的 zip 文件

  - `unzip mytest.zip`，对 mytest.zip 这个文件进行解压，解压到当前所在目录
  - `unzip mytest.zip -d /opt/setups/`，对 mytest.zip 这个文件进行解压，解压到 /opt/setups/ 目录下

- `tar -cvf mytest.tar mytest/`，对 mytest/ 目录进行归档处理（归档和压缩不一样）

- ```
  tar -xvf mytest.tar
  ```

  ，释放 mytest.tar 这个归档文件，释放到当前目录

  - `tar -xvf mytest.tar -C /opt/setups/`，释放 mytest.tar 这个归档文件，释放到 /opt/setups/ 目录下

- `last`，显示最近登录的帐户及时间

- `lastlog`，显示系统所有用户各自在最近登录的记录，如果没有登录过的用户会显示 **从未登陆过**

- ```
  ls
  ```

  ，列出当前目录下的所有没有隐藏的文件 / 文件夹。

  - `ls -a`，列出包括以.号开头的隐藏文件 / 文件夹（也就是所有文件）
  - `ls -R`，显示出目录下以及其所有子目录的文件 / 文件夹（递归地方式，不显示隐藏的文件）
  - `ls -a -R`，显示出目录下以及其所有子目录的文件 / 文件夹（递归地方式，显示隐藏的文件）
  - `ls -al`，列出目录下所有文件（包含隐藏）的权限、所有者、文件大小、修改时间及名称（也就是显示详细信息）
  - `ls -ld 目录名`，显示该目录的基本信息
  - `ls -t`，依照文件最后修改时间的顺序列出文件名。
  - `ls -F`，列出当前目录下的文件名及其类型。以 **/** 结尾表示为目录名，以 ***** 结尾表示为可执行文件，以 **@** 结尾表示为符号连接
  - `ls -lg`，同上，并显示出文件的所有者工作组名。
  - `ls -lh`，查看文件夹类文件详细信息，文件大小，文件修改时间
  - `ls /opt | head -5`，显示 opt 目录下前 5 条记录
  - `ls -l | grep '.jar'`，查找当前目录下所有 jar 文件
  - `ls -l /opt |grep "^-"|wc -l`，统计 opt 目录下文件的个数，不会递归统计
  - `ls -lR /opt |grep "^-"|wc -l`，统计 opt 目录下文件的个数，会递归统计
  - `ls -l /opt |grep "^d"|wc -l`，统计 opt 目录下目录的个数，不会递归统计
  - `ls -lR /opt |grep "^d"|wc -l`，统计 opt 目录下目录的个数，会递归统计
  - `ls -lR /opt |grep "js"|wc -l`，统计 opt 目录下 js 文件的个数，会递归统计
  - `ls -l`，列出目录下所有文件的权限、所有者、文件大小、修改时间及名称（也就是显示详细信息，不显示隐藏文件）。显示出来的效果如下：

```
-rwxr-xr-x. 1 root root 4096 3月 26 10:57，其中最前面的 - 表示这是一个普通文件
lrwxrwxrwx. 1 root root 4096 3月 26 10:57，其中最前面的 l 表示这是一个链接文件，类似 Windows 的快捷方式
drwxr-xr-x. 5 root root 4096 3月 26 10:57，其中最前面的 d 表示这是一个目录
```

- ```
  cd
  ```

  ，目录切换

  - `cd ..`，改变目录位置至当前目录的父目录(上级目录)。
  - `cd ~`，改变目录位置至用户登录时的工作目录。
  - `cd 回车`，回到家目录
  - `cd -`，上一个工作目录
  - `cd dir1/`，改变目录位置至 dir1 目录下。
  - `cd ~user`，改变目录位置至用户的工作目录。
  - `cd ../user`，改变目录位置至相对路径user的目录下。
  - `cd /../..`，改变目录位置至绝对路径的目录位置下。

- ```
  cp 源文件 目标文件
  ```

  ，复制文件

  - `cp -r 源文件夹 目标文件夹`，复制文件夹
  - `cp -r -v 源文件夹 目标文件夹`，复制文件夹(显示详细信息，一般用于文件夹很大，需要查看复制进度的时候)
  - `cp /usr/share/easy-rsa/2.0/keys/{ca.crt,server.{crt,key},dh2048.pem,ta.key} /etc/openvpn/keys/`，复制同目录下花括号中的文件

- `tar cpf - . | tar xpf - -C /opt`，复制当前所有文件到 /opt 目录下，一般如果文件夹文件多的情况下用这个更好，用 cp 比较容易出问题

- ```
  mv 文件 目标文件夹
  ```

  ，移动文件到目标文件夹

  - `mv 文件`，不指定目录重命名后的名字，用来重命名文件

- `touch 文件名`，创建一个空白文件/更新已有文件的时间(后者少用)

- `mkdir 文件夹名`，创建文件夹

- `mkdir -p /opt/setups/nginx/conf/`，创建一个名为 conf 文件夹，如果它的上级目录 nginx 没有也会跟着一起生成，如果有则跳过

- `rmdir 文件夹名`，删除文件夹(只能删除文件夹里面是没有东西的文件夹)

- ```
  rm 文件
  ```

  ，删除文件

  - `rm -r 文件夹`，删除文件夹
  - `rm -r -i 文件夹`，在删除文件夹里的文件会提示(要的话,在提示后面输入yes)
  - `rm -r -f 文件夹`，强制删除
  - `rm -r -f 文件夹1/ 文件夹2/ 文件夹3/`删除多个

- ```
  find
  ```

  ，高级查找

  - `find . -name *lin*`，其中 . 代表在当前目录找，-name 表示匹配文件名 / 文件夹名，*lin* 用通配符搜索含有lin的文件或是文件夹
  - `find . -iname *lin*`，其中 . 代表在当前目录找，-iname 表示匹配文件名 / 文件夹名（忽略大小写差异），*lin* 用通配符搜索含有lin的文件或是文件夹
  - `find / -name *.conf`，其中 / 代表根目录查找，*.conf代表搜索后缀会.conf的文件
  - `find /opt -name .oh-my-zsh`，其中 /opt 代表目录名，.oh-my-zsh 代表搜索的是隐藏文件 / 文件夹名字为 oh-my-zsh 的
  - `find /opt -type f -iname .oh-my-zsh`，其中 /opt 代表目录名，-type f 代表只找文件，.oh-my-zsh 代表搜索的是隐藏文件名字为 oh-my-zsh 的
  - `find /opt -type d -iname .oh-my-zsh`，其中 /opt 代表目录名，-type d 代表只找目录，.oh-my-zsh 代表搜索的是隐藏文件夹名字为 oh-my-zsh 的
  - `find . -name "lin*" -exec ls -l {} \;`，当前目录搜索lin开头的文件，然后用其搜索后的结果集，再执行ls -l的命令（这个命令可变，其他命令也可以），其中 -exec 和 {} ; 都是固定格式
  - `find /opt -type f -size +800M -print0 | xargs -0 du -h | sort -nr`，找出 /opt 目录下大于 800 M 的文件
  - `find / -name "*tower*" -exec rm {} \;`，找到文件并删除
  - `find / -name "*tower*" -exec mv {} /opt \;`，找到文件并移到 opt 目录
  - `find . -name "*" |xargs grep "youmeek"`，递归查找当前文件夹下所有文件内容中包含 youmeek 的文件
  - `find . -size 0 | xargs rm -f &`，删除当前目录下文件大小为0的文件
  - `du -hm --max-depth=2 | sort -nr | head -12`，找出系统中占用容量最大的前 12 个目录

- `cat /etc/resolv.conf`，查看 DNS 设置

- `netstat -tlunp`，查看当前运行的服务，同时可以查看到：运行的程序已使用端口情况

- `env`，查看所有系统变量

- `export`，查看所有系统变量

- ```
  echo
  ```

  - `echo $JAVA_HOME`，查看指定系统变量的值，这里查看的是自己配置的 JAVA_HOME。
  - `echo "字符串内容"`，输出 "字符串内容"
  - `echo > aa.txt`，清空 aa.txt 文件内容（类似的还有：`: > aa.txt`，其中 : 是一个占位符, 不产生任何输出）

- `unset $JAVA_HOME`，删除指定的环境变量

- `ln -s /opt/data /opt/logs/data`，表示给 /opt/logs 目录下创建一个名为 data 的软链接，该软链接指向到 /opt/data

- ```
  grep
  ```

  - `shell grep -H '安装' *.sh`，查找当前目录下所有 sh 类型文件中，文件内容包含 `安装` 的当前行内容
  - `grep 'test' java*`，显示当前目录下所有以 java 开头的文件中包含 test 的行
  - `grep 'test' spring.ini docker.sh`，显示当前目录下 spring.ini docker.sh 两个文件中匹配 test 的行

- ```
  ps
  ```

  - `ps –ef|grep java`，查看当前系统中有关 java 的所有进程
  - `ps -ef|grep --color java`，高亮显示当前系统中有关 java 的所有进程

- ```
  kill
  ```

  - `kill 1234`，结束 pid 为 1234 的进程
  - `kill -9 1234`，强制结束 pid 为 1234 的进程（慎重）
  - `killall java`，结束同一进程组内的所有为 java 进程
  - `ps -ef|grep hadoop|grep -v grep|cut -c 9-15|xargs kill -9`，结束包含关键字 hadoop 的所有进程

- ```
  head
  ```

  - `head -n 10 spring.ini`，查看当前文件的前 10 行内容

- ```
  tail
  ```

  - `tail -n 10 spring.ini`，查看当前文件的后 10 行内容
  - `tail -200f 文件名`，查看文件被更新的新内容尾 200 行，如果文件还有在新增可以动态查看到（一般用于查看日记文件）

## 用户、权限-相关命令

- 使用 pem 证书登录：

  ```
  ssh -i /opt/mykey.pem root@192.168.0.70
  ```

  - 证书权限不能太大，不然无法使用：`chmod 600 mykey.pem`

- `hostname`，查看当前登陆用户全名

- `cat /etc/group`，查看所有组

- `cat /etc/passwd`，查看所有用户

- `groups youmeek`，查看 youmeek 用户属于哪个组

- `useradd youmeek -g judasn`，添加用户并绑定到 judasn 组下

- ```
  userdel -r youmeek
  ```

  ，删除名字为 youmeek 的用户

  - 参数：`-r`，表示删除用户的时候连同用户的家目录一起删除

- 修改普通用户 youmeek 的权限跟 root 权限一样：

  - 常用方法（原理是把该用户加到可以直接使用 sudo 的一个权限状态而已）：

    - 编辑配置文件：`vim /etc/sudoers`
    - 找到 98 行（预估），有一个：`root ALL=(ALL) ALL`，在这一行下面再增加一行，效果如下：

    ```
     root    ALL=(ALL)   ALL
     youmeek    ALL=(ALL)   ALL
    ```

  - 另一种方法：

    - 编辑系统用户的配置文件：`vim /etc/passwd`，找到 **root** 和 **youmeek** 各自开头的那一行，比如 root 是：`root:x:0:0:root:/root:/bin/zsh`，这个代表的含义为：*用户名:密码:UserId:GroupId:描述:家目录:登录使用的 shell*
    - 通过这两行对比，我们可以直接修改 youmeek 所在行的 UserId 值 和 GroupId 值，都改为 0。

- `groupadd judasn`，添加一个名为 judasn 的用户组

- `groupdel judasn`，删除一个名为 judasn 的用户组（前提：先删除组下面的所有用户）

- `usermod 用户名 -g 组名`，把用户修改到其他组下

- `passwd youmeek`，修改 youmeek 用户的密码（前提：只有 root 用户才有修改其他用户的权限，其他用户只能修改自己的）

- ```
  chmod 777 文件名/目录
  ```

  ，给指定文件增加最高权限，系统中的所有人都可以进行读写。

  - linux 的权限分为 rwx。r 代表：可读，w 代表：可写，x 代表：可执行
  - 这三个权限都可以转换成数值表示，r = 4，w = 2，x = 1，- = 0，所以总和是 7，也就是最大权限。第一个 7 是所属主（user）的权限，第二个 7 是所属组（group）的权限，最后一位 7 是非本群组用户（others）的权限。
  - `chmod -R 777 目录` 表示递归目录下的所有文件夹，都赋予 777 权限
  - `chown myUsername:myGroupName myFile` 表示修改文件所属用户、组
  - `chown -R myUsername:myGroupName myFolder` 表示递归修改指定目录下的所有文件权限

- ```
  su
  ```

  ：切换到 root 用户，终端目录还是原来的地方（常用）

  - `su -`：切换到 root 用户，其中 **-** 号另起一个终端并切换账号
  - `su 用户名`，切换指定用户帐号登陆，终端目录还是原来地方。
  - `su - 用户名`，切换到指定用户帐号登陆，其中 **-** 号另起一个终端并切换账号

- `exit`，注销当前用户（常用）

- `sudo 某个命令`，使用管理员权限使用命令，使用 sudo 回车之后需要输入当前登录账号的密码。（常用）

- `passwd`，修改当前用户密码（常用）

- 添加临时账号，并指定用户根目录，并只有可读权限方法

  - 添加账号并指定根目录（用户名 tempuser）：`useradd -d /data/logs -m tempuser`
  - 设置密码：`passwd tempuser` 回车设置密码
  - 删除用户（该用户必须退出 SSH 才能删除成功），也会同时删除组：`userdel tempuser`

## 磁盘管理

- ```
  df -h
  ```

  ，自动以合适的磁盘容量单位查看磁盘大小和使用空间

  - `df -k`，以磁盘容量单位 K 为数值结果查看磁盘使用情况
  - `df -m`，以磁盘容量单位 M 为数值结果查看磁盘使用情况

- `du -sh /opt`，查看 opt 这个文件夹大小 （h 的意思 human-readable 用人类可读性较好方式显示，系统会自动调节单位，显示合适大小的单位）

- `du -sh ./*`，查看当前目录下所有文件夹大小 （h 的意思 human-readable 用人类可读性较好方式显示，系统会自动调节单位，显示合适大小的单位）

- `du -sh /opt/setups/`，显示 /opt/setups/ 目录所占硬盘空间大小（s 表示 –summarize 仅显示总计，即当前目录的大小。h 表示 –human-readable 以 KB，MB，GB 为单位，提高信息的可读性）

- ```
  mount /dev/sdb5 /newDir/
  ```

  ，把分区 sdb5 挂载在根目录下的一个名为 newDir 的空目录下，需要注意的是：这个目录最好为空，不然已有的那些文件将看不到，除非卸载挂载。

  - 挂载好之后，通过：`df -h`，查看挂载情况。

- ```
  umount /newDir/
  ```

  ，卸载挂载，用目录名

  - 如果这样卸载不了可以使用：`umount -l /newDir/`

- `umount /dev/sdb5`，卸载挂载，用分区名

## wget 下载文件

- 常规下载：`wget http://www.gitnavi.com/index.html`
- 自动断点下载：`wget -c http://www.gitnavi.com/index.html`
- 后台下载：`wget -b http://www.gitnavi.com/index.html`
- 伪装代理名称下载：`wget --user-agent="Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US) AppleWebKit/534.16 (KHTML, like Gecko) Chrome/10.0.648.204 Safari/534.16" http://www.gitnavi.com/index.html`
- 限速下载：`wget --limit-rate=300k http://www.gitnavi.com/index.html`
- 批量下载：`wget -i /opt/download.txt`，一个下载地址一行
- 后台批量下载：`wget -b -c -i /opt/download.txt`，一个下载地址一行

## 资料

- http://wenku.baidu.com/view/1ad19bd226fff705cc170af3.html
- http://blog.csdn.net/nzing/article/details/9166057
- http://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/wget.html

# Bash 其他常用命令

## 其他常用命令

- 编辑 hosts 文件：`vim /etc/hosts`，添加内容格式：`127.0.0.1 www.youmeek.com`
- RPM 文件操作命令：
  - 安装
    - `rpm -i example.rpm`，安装 example.rpm 包
    - `rpm -iv example.rpm`，安装 example.rpm 包并在安装过程中显示正在安装的文件信息
    - `rpm -ivh example.rpm`，安装 example.rpm 包并在安装过程中显示正在安装的文件信息及安装进度
  - 查询
    - `rpm -qa | grep jdk`，查看 jdk 是否被安装
    - `rpm -ql jdk`，查看 jdk 是否被安装
  - 卸载
    - `rpm -e jdk`，卸载 jdk（一般卸载的时候都要先用 rpm -qa 看下整个软件的全名）
- YUM 软件管理：
  - `yum install -y httpd`，安装 apache
  - `yum remove -y httpd`，卸载 apache
  - `yum info -y httpd`，查看 apache 版本信息
  - `yum list --showduplicates httpd`，查看可以安装的版本
  - `yum install httpd-查询到的版本号`，安装指定版本
  - 更多命令可以看：http://man.linuxde.net/yum
- 查看某个配置文件，排除掉里面以 # 开头的注释内容：
  - `grep '^[^#]' /etc/openvpn/server.conf`
- 查看某个配置文件，排除掉里面以 # 开头和 ; 开头的注释内容：
  - `grep '^[^#;]' /etc/openvpn/server.conf`

## 资料

- https://www.jianshu.com/p/180fb11a5b96

# Linux 下常用压缩文件的解压、压缩

## 常用压缩包--解压--令整理

- Linux 后缀为 `.war` 格式的文件（一般用在部署 Tomcat 项目的时候）
- 命令：`unzip -oq XXXXXX.war -d ROOT`
  - 如果没有 ROOT 目录会自动创建 ROOT 目录。
- Linux 后缀为 `.tar.gz` 格式的文件-解压
- 命令：`tar zxvf XXXXXX.tar.gz`
- Linux 后缀为 `.bz2` 格式的文件-解压
- 命令：`bzip2 -d XXXXXX.bz2`
- Linux 后缀为 `.tar.bz2` 格式的文件-解压
- 命令：`tar jxvf XXXXXX.tar.bz2`
- Linux 后缀为 `.tar` 格式的文件-解压
- 命令：`tar zxvf XXXXXX.tar`
- Linux 后缀为 `.gz` 格式的文件-解压
- 命令：`gunzip XXXXXX.gz`
- Linux 后缀为 `.zip` 格式的文件-解压
- 命令：`unzip XXXXXX.zip`
- 命令：`unzip XXXXXX.zip -d /opt/`，解压到指定目录
- Linux 后缀为 `.7z` 格式的文件-解压
- 命令：`7za x XXXXXX.7z`
- Linux 后缀为 `.tar.xz` 格式的文件-解压，解压出来是tar，再对tar进行解压
- 命令：`tar xf XXXXXX.tar.xz`

------

## 常用文件进行--压缩--命令整理

- Linux 压缩文件夹为后缀 `.war` 格式的文件（最好不要对根目录进行压缩，不然会多出一级目录）
- 命令：`jar -cvfM0 cas.war /opt/cas/META-INF /opt/cas/WEB-INF /opt/cas/index.jsp`
- 或者命令：`cd 项目根目录 ; jar -cvfM0 cas.war ./*`
- Linux 压缩文件为后缀 `.tar` 格式的文件
- 命令：`tar -zcvf test11.tar test11`
- Linux 压缩文件为后缀 `.tar.gz` 格式的文件
- 命令：`tar -zcvf test11.tar.gz test11`
- Linux 压缩文件为后缀 `.bz2` 格式的文件
- 命令：`bzip2 -v test.txt`
- Linux 压缩文件为后缀 `.tar.bz2` 格式的文件
- 命令：`tar -jcvf test11.tar.gz test11`
- Linux 压缩文件为后缀 `.zip` 格式的文件
- 命令：`zip -r test1.zip /opt/test1/`
- Linux 压缩文件为后缀 `.7z` 格式的文件
- 命令：`7za a test1.7z /opt/test1/`

## 分卷压缩

- 分卷压缩：`zip -s 100M myFile.zip --out newFile.zip`
- 最终效果：

```
newFile.z01
newFile.z02
newFile.z03
newFile.z04
newFile.zip
```

## 特殊格式

- 7z
  - 7z 的安装：
    - 访问官网下载解压包：http://sourceforge.net/projects/p7zip/files/p7zip/
    - 解压压缩包：`tar jxvf p7zip_15.14_src_all.tar.bz2`
    - 进入目录：`cd p7zip_15.14`
    - 执行安装：`sh install.sh`
- rar
  - rar 的安装：
    - 下载：`wget http://www.rarlab.com/rar/rarlinux-3.8.0.tar.gz`
    - 解压下载下来的压缩包：`tar zxvf rarlinux-3.8.0.tar.gz`
    - 进入解压后目录：`cd rar`
    - 编译：`make`
    - 安装：`make install`
  - rar 解压：`rar x 文件名.rar`

## jar 包操作

### 修改 jar 包配置文件

- 命令：`vim mytest.jar`，这时候会展示 jar 中所有层级目录下的所有文件
- 输入：`/log4j2.xml` 回车，光标定位到该文件，然后再回车，进入编辑该文件状态
- 此时可以修改配置文件了，修改后 `:wq` 保存退出，接着 `：q` 退出 jar 编辑状态

### 更新 Jar 包中的文件

- 替换（新增）jar 根目录下的文件：`jar uvf mytest.jar ClassToAdd.class`

- 一般 class 文件都是在多层目录里面的，需要这样做：

  ```
  jar uvf mytest.jar com/youmeek/ClassToAdd.class
  ```

  - 需要在 jar 所在的文件夹下创建：`mkdir -p ./com/youmeek`，该目录必须和原 jar 里面的层级目录结构一致

## 资料

- http://forum.ubuntu.org.cn/viewtopic.php?f=50&t=158893

```
Ubuntu下可以通过：apt-get install <package>安装
CentOS下可以通过：sudo yum install <package>安装
```

作者：内向的牛油果爱读书
链接：https://www.nowcoder.com/discuss/1081094?type=2&channel=-1&source_id=discuss_terminal_discuss_hot_nctrack
来源：牛客网

# 专题

1、绝对路径用什么符号表示？当前目录、上层目录用什么表示？主目录用什么表示? 切换目录用什么命令？   

​    2、使用什么命令查看 ip 地址及接口信息？   

​    3、怎么清屏？怎么退出当前命令？怎么执行睡眠？怎么查看当   

​    4、通过什么命令指定命令提示符?   

​    5、查看文件有哪些命令   

```bash
cat：由第一行开始显示内容，并将所有内容输出
tac：从最后一行倒序显示内容，并将所有内容输出
more：根据窗口大小，一页一页的显示文件内容
less：和more类似，但其优点可以往前翻页，而且进行可以搜索字符
head：只显示头几行
tail：只显示最后几行
nl：类似于cat -n，显示时输出行号
tailf：类似于tail -f
```

​    6、列举几个常用的 Linux 命令   

​    7、怎么对命令进行取别名？   

```
alias
```

​    8、建立软链接(快捷方式)，以及硬链接的命令   

```shell
软链接

说明：软链接仅仅包含所链接文件的路径名，因此能链接目录文件，也可以跨越文件系统进行链接。但是，当原始文件被删除后，链接文件也将失效。
1.软链接，以路径的形式存在。类似于Windows操作系统中的快捷方式
2.软链接可以跨文件系统 ，硬链接不可以
3.软链接可以对一个不存在的文件名进行链接
4.软链接可以对目录进行链接

建立软链接：ln -s 源文件或目录 目标文件或目录
ln -s /usr/local/nginx/sbin/nginx /usr/bin/nginx

硬链接：

说明：可以将硬链接理解为一个“指向原始文件inode的指针”，系统不为它分配独立的inode和文件。所以，硬链接文件与原始文件其实是同一个文件，只不过是不同的名字而已。我们每添加一个硬链接，该文件的inode链接数就会增加1；而且只有当该文件的inode连接数为0时，才算彻底将它删除。换言之，由于硬链接实际上是指向原文件的inode的指针，因此即便原始文件被删除，依然可以通过硬链接文件来访问。
1.硬链接，以文件副本的形式存在。但不占用实际空间。
2.不允许给目录创建硬链接
3.硬链接只有在同一个文件系统中才能创建
[root@CentOS6 project]# echo "Hello world" > readme.txt
[root@CentOS6 project]# ln readme.txt readit.txt	#创建一个硬链接
[root@CentOS6 project]# cat readme.txt
Hello world
[root@CentOS6 project]# cat readit.txt
Hello world
[root@CentOS6 project]# ls -l readme.txt
-rw-r--r--. 2 root root 12 Mar 16 23:41 readme.txt
[root@CentOS6 project]# rm -rf readme.txt	#删除原文件
[root@CentOS6 project]# cat readit.txt	#删除原文件之后readit.txt依旧可以访问
Hello world
[root@CentOS6 project]# ls -l readit.txt
-rw-r--r--. 1 root root 12 Mar 16 23:41 readit.txt

```

​    9、当你需要给命令绑定一个宏或者按键的时候，应该怎么做呢？   

​    10、查看文件内容有哪些命令可以使用？   

​    11、随意写文件命令？怎么向屏幕输出带空格的字符串，比如”hello world”?   

​    12、你的系统目前有许多正在运行的任务，在不重启机器的条件下，有什么方法可以把所有正在运行的进程移除呢？   

​    13、移动文件用哪个命令？改名用哪个命令？   

​    14、复制文件用哪个命令？如果需要连同文件夹一块复制呢？如果需要有提示功能呢？   

​    15、怎样一页一页地查看一个大文件的内容呢？   

​    16、Linux 下命令有哪几种可使用的通配符？分别代表什么含义?   

​    17、用什么命令对一个文件的内容进行统计？(行号、单词数、字节数)   

​    18、Grep 命令有什么用？ 如何忽略大小写？ 如何查找不含该串的行?   

​    19、Linux 中进程有哪几种状态？在 ps 显示出来的信息中分别用什么符号表示的？   

​    20、怎样查看一个 linux 命令的概要与用法？假设你在/bin 目录中偶然看到一个你从没见过的的命令，怎样才能知道它的作用和用法呢？   

​    21、怎么查看当前进程？怎么执行退出？怎么查看当前路径？   

​    22、Ls 命令执行什么功能？ 可以带哪些参数，有什么区别？   

​    23、你平时是怎么查看日志的？   

​    24、终端是哪个文件夹下的哪个文件？黑洞文件是哪个文件夹下的哪个命令？   

​    25、删除文件用哪个命令？如果需要连目录及目录下文件一块删除呢？删除空文件夹用什么命令？   

​    26、怎么使一个命令在后台运行?   

​    27、目录创建用什么命令？创建文件用什么命令？复制文件用什么命令？   

​    28、使用哪一个命令可以查看自己文件系统的磁盘空间配额呢？
