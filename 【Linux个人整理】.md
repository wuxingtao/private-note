<div>

<div>

*   [1\. 系统相关](#)
    *   [更新apt](#)
    *   [安装 gdebi （deb包安装工具）](#)
        *   [安装Mysql](#)
        *   [Ubuntu Navicat for MySQL安装以及破解方案](#)
        *   [设置全局，创建软链接或物理链接（指向文件或目录）](#)
    *   [Hash 校验和不符](#)
    *   [获取文件路径](#)
        *   [查看隐藏文件 (ctrl + H)](#)
        *   [终端命令补全 (Tab)](#)
        *   [添加到启动器 (Exec= bash + filePath)](#)
        *   [<span style="color:red">编译安装</span>](#)
    *   [设置PATH路径,把安装的ruby放在系统PATH前面，避免调用操作系统自带的ruby](#)
    *   [系统变量](#)
        *   *   *   *   [sudo gedit /etc/environment](#)
    *   [用户变量](#)
        *   [添加开机运行脚本](#)
    *   [<span style="color:red">配置软件设置区域</span>](#)
*   [2\. 解压缩 zip unzip tar](#)
    *   [<span style="color:red">TAR</span>](#)
    *   [tar -xvf archive_name.tar -C /tmp/extract_here/](#)
    *   [tar -zcvf archive_name.tar.gz directory_to_compress](#)
    *   [tar -zxvf archive_name.tar.gz](#)
    *   [tar -zxvf archive_name.tar.gz -C /tmp/extract_here/](#)
    *   [tar -jcvf archive_name.tar.bz2 directory_to_compress](#)
    *   [tar -jxvf archive_name.tar.bz2 -C /tmp/extract_here/](#)
    *   [<span style="color:red">ZIP</span>](#)
    *   [zip -r archive_name.zip directory_to_compress](#)
    *   [unzip archive_name.zip](#)
        *   [<span style="color:red">unbuntu 解压zip 乱码</span>](#)
    *   [7z](#)
*   [权限管理](#)
    *   [一、chmod的用法](#)
    *   [二、chown 命令](#)
*   [驱动](#)
*   [3.常用命令](#)
    *   [查找文件位置](#)
*   [音频设置 alsamixer](#)
*   [Centos 系统](#)
    *   [软件安装](#)
        *   [Node安装](#)
        *   [centos Mysql安装](#)

</div>

<div><a name="120e7b3bbe7bb9fe79bb8e585b3_1" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

# 1\. 系统相关

<div><a name="e69bb4e696b0apt_2" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## 更新apt

1.  apt-get update
2.  apt-get upgrade upgrade只是简单的更新包，不管这些依赖，它不和添加包，或是删除包
3.  apt-get dist-upgrade dist-upgrade可以根据依赖关系的变化，添加包，删除包。

<div><a name="e5ae89e8a38520gdebi20efbc88debe58c85e5ae89e8a385e5b7a5e585b7efbc89_3" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## 安装 gdebi （deb包安装工具）

<div style="margin-top: 1em; margin-right: 0px; margin-bottom: 1em; margin-left: 0px; position: relative; padding-bottom: 2em;">

```
sudo apt-get install gdebi
wget packages.linuxmint.com/pool/main/m/mintdrivers/mintdrivers_1.1.4_all.deb
sudo gdebi mintdrivers_1.1.4_all.deb

```

</div>

<div><a name="e5ae89e8a385mysql_4" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

### 安装Mysql

1.从官网下载 MySQL APT Repository
sudo dpkg -i mysql-apt-config_0.8.0-1_all.deb

--recursive（或者-R），可以改变安装的默认路径。
使用方式是：dpkg -i(或者--install) xxx.deb -R /dir/dir2
sudo dpkg -i \xx\[package.name](http://package.name) -r \\

2.更新源
sudo apt-get update

3.安装MySQL服务器
sudo apt-get install mysql-server

4.查看MySQL服务是否启动
netstat -tap | grep mysql

5.查看MySQL相关位置
whereis mysql
(/etc/mysql目录下存放mysql的配置文件my.cnf。用户可根据需要配置。)

6.修改MySQL-Server字符集
找到配置文件/etc/mysql/my.cnf，或其相关文件

在[mysqld]下添加

character-set-server=utf8

重启MySQL服务
service mysql restart

7.登陆MySQL
mysql -u root -p

8.修改MySQL-Client字符集
mysql> charset utf8

9.查看状态
mysql> status

<div><a name="ubuntu20navicat20for20mysqle5ae89e8a385e4bba5e58f8ae7a0b4e8a7a3e696b9e6a188_5" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

### Ubuntu Navicat for MySQL安装以及破解方案

今天安装了Navicat for MySQL有LINUX版本了哈， 开心的说，
首先上官网上下载LINUX版本： [http://www.navicat.com/download/navicat-for-mysql](http://www.navicat.com/download/navicat-for-mysql)

1.  下载 navicat110_mysql_en.tar.gz 文件

2.  下载后解压tar文件

tar -zxvf /home/rain/download/navicat8_mysql_en.tar.gz

1.  解压后 进入解压后的目录运行命令：
    ./start_navicat
    OK，这样就完啦

连接上数据库后里面的中文数据是乱码,把Ubuntu的字符集修改为zh_CN.utf8就行了,修改方法:

1.查看系统支持的字符集: locale -a

2,修改字符集: export.utf8

<span style="color: red; font-weight: bold;">破解方案：</span>

第一次执行start_navicat时，会在用户主目录下生成一个名为.navicat的隐藏文件夹。

cd /home/rain/.navicat/
此文件夹下有一个system.reg文件

rm system.reg

把此文件删除后，下次启动navicat 会重新生成此文件，30天试用期会按新的时间开始计算。

<div><a name="e8aebee7bdaee585a8e5b180efbc8ce5889be5bbbae8bdafe993bee68ea5e68896e789a9e79086e993bee68ea5efbc88e68c87e59091e69687e4bbb6e68896e79baee5bd95efbc89_6" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

### 设置全局，创建软链接或物理链接（指向文件或目录）

tar.gz安装后

<div style="margin-top: 1em; margin-right: 0px; margin-bottom: 1em; margin-left: 0px; position: relative; padding-bottom: 2em;">

```
ln -s file1 lnk1 创建一个指向文件或目录的软链接
ln file1 lnk1 创建一个指向文件或目录的物理链接 

```

</div>

<div style="margin-top: 1em; margin-right: 0px; margin-bottom: 1em; margin-left: 0px; position: relative; padding-bottom: 2em;">

```
//demo node设置全局
ln -s /home/kun/mysofltware/node-v0.10.28-linux-x64/bin/node /usr/local/bin/node
ln -s /home/kun/mysofltware/node-v0.10.28-linux-x64/bin/npm /usr/local/bin/npm

```

</div>

<div><a name="hash20e6a0a1e9aa8ce5928ce4b88de7aca6_7" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## Hash 校验和不符

**1\. 清除临时文件**

<div style="margin-top: 1em; margin-right: 0px; margin-bottom: 1em; margin-left: 0px; position: relative; padding-bottom: 2em;">

```
sudo apt-get clean
sudo rm -rf /var/lib/apt/lists/*

```

</div>

执行了以上命令后，再执行 update&&upgrade 命令试试，是不是OK了？
一般在运行upgrade或dist-upgrade之间，要运行update.

**2\. 选择更优的软件源（服务器）**
在 系统设置 里，找到 软件和更新 ，在 Ubuntu软件 这个选项卡里有个 源代码 下载自 ，将其选为 其他 ，即会弹出如下图所示的服务器列表。

我们也不知道哪个源更好。

点击 选择最佳服务器 按钮，让它自己去选择。

**P.S. 最好，将第一步的清除临时文件的命令再执行一遍。**

* * *

<div><a name="e88eb7e58f96e69687e4bbb6e8b7afe5be84_8" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## 获取文件路径

1.  可视化界面查看（ctrl + L）。
2.  直接在终端输入pwd

<div><a name="e69fa5e79c8be99a90e8978fe69687e4bbb620ctrl2020h_9" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

### 查看隐藏文件 (ctrl + H)

<div><a name="e7bb88e7abafe591bde4bba4e8a1a5e585a82020tab_10" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

### 终端命令补全 (Tab)

如: sublime_text (sublime,sub,sulm)

<div><a name="e6b7bbe58aa0e588b0e590afe58aa8e599a820exec20bash2020filepath_11" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

### 添加到启动器 (Exec= bash + filePath)

Exec=bash /usr/local/share/robomongo-0.9.0-rc8-linux-x86_64-c113244/bin/robomongo

**eclipse快捷方式的创建**

1、进入/usr/share/applications目录

root@PC:/usr/share/applications#

2、gedit创建一个eclipse.desktop文件

root@PC:/usr/share/applications# gedit eclipse.desktop

3、写入以下内容，并保存

[Desktop Entry]
Version=1.0
Name=eclipse
Exec=/home/XXXXXX/adt-bundle-linux-x86_64-20140702/eclipse/eclipse
Terminal=false
Icon=/home/XXXXXX/adt-bundle-linux-x86_64-20140702/eclipse/icon.xpm
Type=Application
Categories=Development

注意： Exec=和Icon=请替换成本地目录。
4、这时就可以在搜索中找到eclpise程序了，直接拖拽到启动器上即可。

<div><a name="e7bc96e8af91e5ae89e8a385_12" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

### <span style="color: red;">编译安装</span>

./configure (--prefix=安装位置）
make (编译)
make install
（make && make install）

<div><a name="e8aebee7bdaepathe8b7afe5be84e68a8ae5ae89e8a385e79a84rubye694bee59ca8e7b3bbe7bb9fpathe5898de99da2efbc8ce981bfe5858de8b083e794a8e6938de4bd9ce7b3bbe7bb9fe887aae5b8a6e79a84ruby_13" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## 设置PATH路径,把安装的ruby放在系统PATH前面，避免调用操作系统自带的ruby

<div style="margin-top: 1em; margin-right: 0px; margin-bottom: 1em; margin-left: 0px; position: relative; padding-bottom: 2em;">

```
export PATH=/usr/local/ruby-1.9.1/bin:$PATH

```

</div>

<div><a name="e7b3bbe7bb9fe58f98e9878f_14" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## 系统变量

1.打开终端并输入：

<div><a name="sudo20gedit20etcenvironment_15" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

###### sudo gedit /etc/environment

（输入用户密码。这时输入的密码是不可见的。）

如图，在PATH="...."的末尾处添加：
：/opt/EmbedSky/4.3.3/bin

其中/opt/EmbedSky/4.3.3/bin为你自己需要设置的环境变量路径。

2.使其立即生效，在终端执行：
source /etc/environment
或者重启电脑即可。

<div><a name="e794a8e688b7e58f98e9878f_16" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## 用户变量

打开终端并输入：

######sudo gedit ~/.bashrc。

前面的步骤会打开.bashrc文件，在其末尾添加：
export PATH=/opt/EmbedSky/4.3.3/bin:$PATH

使其立即生效，在终端执行：
source ~/.bashrc

<div><a name="e6b7bbe58aa0e5bc80e69cbae8bf90e8a18ce8849ae69cac_17" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

### 添加开机运行脚本

先设置此文件可执行：
#####chmod +x /home/xx/x.sh
再加入自动执行脚本：
#####sudo vi /etc/rc.local
在exit 0的上面新起一行，写入/home/xx/x.sh

###不能访问盘符，被windows占用修复 （sudo ntfsfix /dev/sda*）
######## sudo ntfsfix /dev/sda8

<div><a name="e9858de7bdaee8bdafe4bbb6e8aebee7bdaee58cbae59f9f_18" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## <span style="color: red;">配置软件设置区域</span>

右键终端：直接安装一个软件包nautilus-open-terminal

<div><a name="220e8a7a3e58e8be7bca920zip20unzip20tar_19" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

# 2\. 解压缩 zip unzip tar

<div style="margin-top: 1em; margin-right: 0px; margin-bottom: 1em; margin-left: 0px; position: relative; padding-bottom: 2em;">

```
//tar命令
-A或--catenate：新增文件到以存在的备份文件； 
-B：设置区块大小； 
-c或--create：建立新的备份文件； 
-C <目录>：这个选项用在解压缩，若要在特定目录解压缩，可以使用这个选项。 
-d：记录文件的差别； 
-x或--extract或--get：从备份文件中还原文件；
-t或--list：列出备份文件的内容；
-z或--gzip或--ungzip：通过gzip指令处理备份文件； 
-Z或--compress或--uncompress：通过compress指令处理备份文件；
-f<备份文件>或--file=<备份文件>：指定备份文件；
 -v或--verbose：显示指令执行过程； -r：添加文件到已经压缩的文件； 
-u：添加改变了和现有的文件到已经存在的压缩文件； 
-j：支持bzip2解压文件； 
-v：显示操作过程； 
-l：文件系统边界设置； 
-k：保留原有文件不覆盖； -m：保留文件不被覆盖；
 -w：确认压缩文件的正确性；
-p或--same-permissions：用原来的文件权限还原文件； 
-P或--absolute-names：文件名使用绝对名称，不移除文件名称前的“/”号； 
-N <日期格式> 或 --newer=<日期时间>：只将较指定日期更新的文件保存到备份文件里； --exclude=<范本样式>：排除符合范本样式的文件。

来自: http://man.linuxde.net/tar

```

</div>

<div><a name="tar_20" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## <span style="color: red;">TAR</span>

Tar是在Linux中使用得非常广泛的文档打包格式。它的好处就是它只消耗非常少的CPU以及时间去打包文件，他仅仅只是一个打包工具，并不负责压缩。下面是如何打包一个目录：

`tar -cvf archive_name.tar directory_to_compress`

如何解包：

tar -xvf archive_name.tar.gz

上面这个解包命令将会将文档解开在当前目录下面。当然，你也可以用这个命令来捏住解包的路径：

<div><a name="tar20-xvf20archive_nametar20-c20tmpextract_here_21" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## tar -xvf archive_name.tar -C /tmp/extract_here/

#<span style="color: red;">TAR.GZ</span>

这种格式是我使用得最多的压缩格式。它在压缩时不会占用太多CPU的，而且可以得到一个非常理想的压缩率。使用下面这种格式去压缩一个目录：

<div><a name="tar20-zcvf20archive_nametargz20directory_to_compress_22" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## tar -zcvf archive_name.tar.gz directory_to_compress

解压缩：

<div><a name="tar20-zxvf20archive_nametargz_23" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## tar -zxvf archive_name.tar.gz

上面这个解包命令将会将文档解开在当前目录下面。当然，你也可以用这个命令来捏住解包的路径：

<div><a name="tar20-zxvf20archive_nametargz20-c20tmpextract_here_24" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## tar -zxvf archive_name.tar.gz -C /tmp/extract_here/

#<span style="color: red;">TAR.BZ2</span>

这种压缩格式是我们提到的所有方式中压缩率最好的。当然，这也就意味着，它比前面的方式要占用更多的CPU与时间。这个就是你如何使用tar.bz2进行压缩。

<div><a name="tar20-jcvf20archive_nametarbz220directory_to_compress_25" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## tar -jcvf archive_name.tar.bz2 directory_to_compress

上面这个解包命令将会将文档解开在当前目录下面。当然，你也可以用这个命令来捏住解包的路径：

<div><a name="tar20-jxvf20archive_nametarbz220-c20tmpextract_here_26" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## tar -jxvf archive_name.tar.bz2 -C /tmp/extract_here/

<div><a name="zip_27" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## <span style="color: red;">ZIP</span>

zip可能是目前使用得最多的文档压缩格式。它最大的优点就是在不同的操作系统平台，比如Linux， Windows以及Mac OS，上使用。缺点就是支持的压缩率不是很高，而tar.gz和tar.gz2在压缩率方面做得非常好。闲话少说，我们步入正题吧：

我们可以使用下列的命令压缩一个目录：

<div><a name="zip20-r20archive_namezip20directory_to_compress_28" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## zip -r archive_name.zip directory_to_compress

下面是如果解压一个zip文档：

<div><a name="unzip20archive_namezip_29" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## unzip archive_name.zip

<div><a name="unbuntu20e8a7a3e58e8bzip20e4b9b1e7a081_30" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

### <span style="color: red;">unbuntu 解压zip 乱码</span>

1.  通过unzip行命令解压，指定字符集
    unzip -O CP936 xxx.zip (用GBK, GB18030也可以)
    有趣的是unzip的manual中并无这个选项的说明, unzip --help对这个参数有一行简单的说明。

<div><a name="7z_31" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## 7z

安装：apt-get install p7zip-full

解压7z：使用方法：7z x file file是你要解压的文件名。

解压tar.bz2: sudo tar -jxvf file.tar.bz2。

解压tar: sudo tar -zxvf file.tar。

<div><a name="e69d83e99990e7aea1e79086_32" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

# 权限管理

<div><a name="e4b880e38081chmode79a84e794a8e6b395_33" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## 一、chmod的用法

指令名称 : chmod
使用权限 : 所有使用者
使用方式 : chmod [-cfvR] [--help] [--version] mode file…
说明 : Linux/Unix 的档案调用权限分为三级 : 档案拥有者、群组、其他。利用 chmod 可以藉以控制档案如何被他人所调用。
参数 :
mode : 权限设定字串，格式如下 : [ugoa...][[+-=][rwxX]…][,...]，其中
u 表示该档案的拥有者，g 表示与该档案的拥有者属于同一个群体(group)者，o 表示其他以外的人，a 表示这三者皆是。

*   表示增加权限、- 表示取消权限、= 表示唯一设定权限。
    r 表示可读取，w 表示可写入，x 表示可执行，X 表示只有当该档案是个子目录或者该档案已经被设定过为可执行。
    -c : 若该档案权限确实已经更改，才显示其更改动作
    -f : 若该档案权限无法被更改也不要显示错误讯息
    -v : 显示权限变更的详细资料
    -R : 对目前目录下的所有档案与子目录进行相同的权限变更(即以递回的方式逐个变更)
    –help : 显示辅助说明
    –version : 显示版本
    范例 :将档案 file1.txt 设为所有人皆可读取 :
    chmod ugo+r file1.txt
    将档案 file1.txt 设为所有人皆可读取 :
    chmod a+r file1.txt
    将档案 file1.txt 与 file2.txt 设为该档案拥有者，与其所属同一个群体者可写入，但其他以外的人则不可写入 :
    chmod ug+w,o-w file1.txt file2.txt
    将 [ex1.py](http://ex1.py) 设定为只有该档案拥有者可以执行 :
    chmod u+x [ex1.py](http://ex1.py)
    将目前目录下的所有档案与子目录皆设为任何人可读取 :
    chmod -R a+r *

###此外chmod也可以用数字来表示权限如 chmod 777 file
语法为：chmod abc file
其中a,b,c各为一个数字，分别表示User、Group、及Other的权限。
r=4，w=2，x=1
若要rwx属性则4+2+1=7；
若要rw-属性则4+2=6；
若要r-x属性则4+1=5。
范例：
chmod a=rwx file
和
chmod 777 file
效果相同
chmod ug=rwx,o=x file
和
chmod 771 file
效果相同
若用chmod 4755 filename可使此程序具有root的权限

<div><a name="e4ba8ce38081chown20e591bde4bba4_34" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## 二、chown 命令

用途：更改文件的所有者或组。命令由单词change owner组合而成。
使用示例：
1，更改文件的所有者：
chown jim program.c
文件 program.c 的所有者更改为 jim。作为所有者，jim 可以使用 chmod 命令允许或拒绝其他用户访问 program.c。
2，更改目录的所有者：
chown -R john:build /tmp/src
将目录 /tmp/src 中所有文件的所有者和组更改为用户 john 和组 build

*   R 递归式地改变指定目录及其下的所有子目录和文件的拥有者。
*   v 显示chown命令所做的工作。

<div><a name="e9a9b1e58aa8_35" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

# 驱动

3、安装显卡驱动
Ubuntu默认的显卡驱动虽然可以让你的计算机显示毫无问题，但是要想发挥显卡的全部性能，就需要安装专有驱动了，别紧张，你只需要在软件和更新里的驱动列表选择合适的驱动安装即可。 Ubuntu 14.04/14.10下风扇高速旋转解决 [http://www.linuxidc.com/Linux/2014-10/108483.htm](http://www.linuxidc.com/Linux/2014-10/108483.htm)
Ubuntu 14.10安装后要做的6件事

<div><a name="3e5b8b8e794a8e591bde4bba4_36" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

# 3.常用命令

<div><a name="e69fa5e689bee69687e4bbb6e4bd8de7bdae_37" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## 查找文件位置

*   locate

<div style="margin-top: 1em; margin-right: 0px; margin-bottom: 1em; margin-left: 0px; position: relative; padding-bottom: 2em;">

```
locate *.deb

```

</div>

*   whereis ***
*   dpkg -l

<div><a name="e99fb3e9a291e8aebee7bdae20alsamixer_38" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

# 音频设置 alsamixer

`sudo alsamixer`
注意，下面有的项是会显示MM的，MM是关闭的意思，按键盘的M键可以打开。
其实每一项的意义都是很明显的，如下图，
Master是主要的音量，
Headphone就是你的耳机的音量（如果开扬声的话，这里就是0或被禁止了），
Speaker就是扬声器了，PCM不知道什么鬼（正常音量水平就好了），
Mic自然就是麦克风了，Mic Boost跟Mic相关的吧，
S/PDIF（关闭就好了），Auto-Mute Mode（自动静音，这个开或关都试一下吧），Loopback（开着吧，不是很清楚是什么）。

`alsactl store` 保存配置

<div><a name="centos20e7b3bbe7bb9f_39" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

# Centos 系统

<div><a name="e8bdafe4bbb6e5ae89e8a385_40" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

## 软件安装

<div><a name="nodee5ae89e8a385_41" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

### Node安装

安装Node.js的方法有许多不像windows系统只有双击安装程序了，那么centos中有几种安装Node.js的方法呢？下面我们来为各位整理4种，希望对各位有帮助。

**一、源码安装**
1.下载源码（官网查看最新版本链接）
wget [http://nodejs.org/dist/v0.10.30/node-v0.10.30.tar.gz](http://nodejs.org/dist/v0.10.30/node-v0.10.30.tar.gz)
2.解压源码
tar xzvf node-v* && cd node-v*
3.安装必要的编译软件
sudo yum install gcc gcc-c++
4.编译
./configure
make
5.编译&安装
sudo make install
6.查看版本（测试安装是否成功）
node --version

**二、使用已编译版本安装**
1.下载已编译版本
最新版本可在官网获得：传送门
cd ~
wget [http://nodejs.org/dist/v0.10.30/node-v0.10.30-linux-x64.tar.gz](http://nodejs.org/dist/v0.10.30/node-v0.10.30-linux-x64.tar.gz)
2.解压
sudo tar --strip-components 1 -xzvf node-v* -C /usr/local
3.老样子，测试安装
node --version

**三、使用EPEL安装**
1.下载EPEL
sudo rpm -i [http://download.fedoraproject.org/pub/epel/beta/7/x86_64/epel-release-7-0.2.noarch.rpm](http://download.fedoraproject.org/pub/epel/beta/7/x86_64/epel-release-7-0.2.noarch.rpm)
2.安装
sudo yum install nodejs
3.老样子，测试安装
node --version
4.（可选）安装npm管理包
sudo yum install npm

**四、通过NVM安装**
NVM（Node version manager）顾名思义，就是Node.js的版本管理软件，可以轻松的在Node.js各个版本间切换，项目源码GitHub
1.下载并安装NVM脚本
curl [https://raw.githubusercontent.com/creationix/nvm/v0.13.1/install.sh](https://raw.githubusercontent.com/creationix/nvm/v0.13.1/install.sh) | bash
source ~/.bash_profile
或
wget -qO- [https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh](https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh) | bash
2.列出所需要的版本
nvm list-remote
返回结果如下
. . .
v0.10.29
v0.10.30
v0.11.0
v0.11.1
v0.11.2
v0.11.3
v0.11.4
v0.11.5
v0.11.6
v0.11.7
v0.11.8
v0.11.9
v0.11.10
v0.11.11
v0.11.12
v0.11.13
3.安装相应的版本
nvm install v0.10.30
4.查看已安装的版本
nvm list
-> v0.10.30
system
5.切换版本
nvm use v0.10.30
6.设置默认版本
nvm alias default v0.10.30

<div><a name="centos20mysqle5ae89e8a385_42" style="color: #0088cc; text-decoration: none;"></a><a style="color: #0088cc; text-decoration: none; float: left; visibility: hidden;"></a></div>

### centos Mysql安装

首先CentOS7 已经不支持mysql，因为收费了你懂得，所以内部集成了mariadb，而安装mysql的话会和mariadb的文件冲突，所以需要先卸载掉mariadb，以下为卸载mariadb，安装mysql的步骤。

#列出所有被安装的rpm package
rpm -qa | grep mariadb

#卸载
rpm -e mariadb-libs-5.5.37-1.el7_0.x86_64
错误：依赖检测失败：
libmysqlclient.so.18()(64bit) 被 (已安裝) postfix-2:2.10.1-6.el7.x86_64 需要
libmysqlclient.so.18(libmysqlclient_18)(64bit) 被 (已安裝) postfix-2:2.10.1-6.el7.x86_64 需要

#强制卸载，因为没有--nodeps
rpm -e --nodeps mariadb-libs-5.5.37-1.el7_0.x86_64

#安装mysql依赖
yum install vim libaio net-tools

其他情况：

1、centos下yum暂时没有mysql-server直接安装包；
MariaDB是MySQL社区开发的分支，也是一个增强型的替代品;

2、安装MariaDB
yum -y install mariadb-server mariadb mariadb-devel
systemctl start mariadb
systemctl enable mariadb
mysql_secure_installation
firewall-cmd --permanent --add-service mysql
systemctl restart firewalld.service
iptables -L -n|grep 3306

CentOS7的yum源中默认好像是没有mysql的。为了解决这个问题，我们要先下载mysql的repo源。

1.  下载mysql的repo源

$ wget [http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm](http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm)

1.  安装mysql-community-release-el7-5.noarch.rpm包

$ sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm

安装这个包后，会获得两个mysql的yum repo源：/etc/yum.repos.d/mysql-community.repo，/etc/yum.repos.d/mysql-community-source.repo。

1.  安装mysql

$ sudo yum install mysql-server

根据步骤安装就可以了，不过安装完成后，没有密码，需要重置密码。

1.  重置密码

重置密码前，首先要登录

$ mysql -u root

登录时有可能报这样的错：ERROR 2002 (HY000): Can‘t connect to local MySQL server through socket ‘/var/lib/mysql/mysql.sock‘ (2)，原因是/var/lib/mysql的访问权限问题。下面的命令把/var/lib/mysql的拥有者改为当前用户：

$ sudo chown -R openscanner:openscanner /var/lib/mysql

然后，重启服务：

$ service mysqld restart

接下来登录重置密码：

$ mysql -u root

mysql > use mysql;

mysql > update user set password=password(‘123456‘) where user=‘root‘;

mysql > exit;

1.  开放3306端口

$ sudo vim /etc/sysconfig/iptables

添加以下内容：

-A INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT

保存后重启防火墙：

$ sudo service iptables restart

这样从其它客户机也可以连接上mysql服务了。

MYSQL启动后报：ERROR! The server quit without updating PID file错误的问题解决
MYSQL日志：Can't find file: './mysql/plugin.frm' (errno: 13 - Permission denied)

1、权限不够：chown -R mysql:mysql /home/mysql/data” “chmod -R 755 /home/mysql/data
2、centos7的selinux问题：打开/etc/selinux/config，把SELINUX=enforcing改为SELINUX=disabled后存盘退出重启机器。

</div>