## 重定向命令

重定向命令也成为输出重定向,把终端命令输出到指定文件当中

> '>'如果文件存在则覆盖文件,相当于py文件操作当中的w模式
>
> '>>'如果文件存在则追加文件末尾,相当py文件操作中的a模式

## 查看&&编辑文本文件内容

cat	适用于查看小型文件

more	适用于查看大型文件 分屏输出,会节省时间,减少主机的资源

>空格	下一屏
>
>回车	下一行
>
>b	上一屏
>
>f	显示下一屏
>
>q	退出

gedit	文件编辑命令,可以查看文件,也可以编辑(相当于win下的记事本)

## 管道符[ | ]

 一个命令的输出可以通过管道作为另一个命令的输入,可以理解为一个容器

一般会结合more使用 分屏显示命令的打印结果

## 链接命令ln

ln -s 	创建软连接

> ln -s 源文件 新建的链接

ln	创建硬链接

> ln 源文件 目标文件

**软链接**相当于windows下的快捷方式,当一个源文件目录层文件比较深,我们想要方便使用可以创建一个软连接

> 如果软链接和源文件不在同一个目录，源文件要使用绝对路径，不能使用相对路径。
> 删除源文件则软链接失效
> 可以给目录创建软链接

**硬链接**就是原文件的一个别名,也就是说这两个文件指向同一个数据

>创建硬链接使用相对路径和绝对路径都可以
>删除源文件，硬链接还可以访问到数据。
>创建硬链接，硬链接数会加1，删除源文件或者硬链接，硬链接数会减1。
>创建软链接，硬链接数不会加1
>不能给目录创建硬链接

## 文本搜索命令

grep [-i] [-n] [-v]	可以对文本进行搜素

-i	忽略大小写
-n	显示匹配行号
-v	取反

### 正则表达式

^	指定字符串开头
$	以指定字符串结尾
.	匹配一个非换行符的字符

#### 文本搜索命令可以搜索管道中的内容

{ls | grebp lib}
在使用grep命令时还可以省略搜索内容的引号例如{ls/|grep lib,grep hello 1.txt

```shell
wc [-l]
	#统计一个文件的行数
```



## find:查找文件

find	在指定文件目录下查找文件(包括目录)
项目:
-name	根据文件名,目录名字查找

### 通配符

"*"	代表0个或者多个任意字符
"?"	代表着任意字符

> 通配符不仅仅可以和find结合使用,同样的ls.mv.cp等.不过find使用通配符必须添加引号

## 解压缩命令

linux支持的压缩文件格式

>.gz
>.bz2
>.zip

.gz和.bz2的压缩包需要使用tar命令来解压缩
.zip的压缩包需要使用zip命令来压缩,使用upzip来解压缩

#### tar命令

tar [-c] [-v] [-f] [-z] [-j] [-x] [-C]
-c	创建打包文件
-v	显示打包或者解包的详细信息
-f	指定文件名称,必须放在所有选项后便
-z	压缩或者解压(.gz)
-j	压缩或者解压(.bz2)
-x	解包
-C	解压缩到指定目录

###### 压缩,gz

> tar -zcvf test.tar.gz *.txt

###### 压缩.bz2

> tar -jcvf text.bz2 *.txt

###### 解压.gz

> tar -zxvf text.tar.gz
>
> tar -zxvf text.tar.gz -C aa /*解压到aa文件夹

###### 解压.bz2

>tar -jxvf text.bz2

#### zip命令

zip	压缩成zip格式文件
unzip	解压缩zip格式文件

-d	指定解压目录

###### 压缩

> zip test.zip *txt

###### 解压

> unzip text.zip

## 文件的权限

chmod	修改文件权限

### 字母

u	user表示该文件的所有者
g	group表示用户组
o	other表示其他用户
a	all,表示所有用户

##### 权限设置

'+'	增加权限
'-'	撤销权限
'='	设置权限

##### 权限说明

r	可读
w	可写
x	可执行|
'-'	无任何权限

chmod u=r,g=-,o=rw 1.txt
当前用户可读,用户组没有权限,其他用户可读可写

### 数字

r	可读 数字为4
w	可写 数字为2
x	可执行 数字为1
'-'	无任何权限 数字为0

## 获取管理员权限的相关命令

sudo -s	切换到root用户,获取管理员权限
sudo	某个命令需要获取管理员权限可在执行之前加上sudo

whoami	查看当前用户权限
exit	退出登录系统++>如果是切换后的用户退出则返回上一个登录账号-->如果是终端界面则退出当前终端

who	查看所有登录账户
passwd	修改用户密码,不指定用户则修改当前用户的密码
which	查看命令的位置
poweroff	关机
shutdown -h now	关机
reboot	重启

## 用户相关操作

userdd	添加用户
-m	自动创建用户主目录,目录名就是用户名
-g	将指定他用户的用户组
id	查看用户信息
passwd	更改密码
su	切换用户
确定用户是否存在

```shell
cat /etc/passwd
```

gpasswd	添加和删除附组

> -a	给用户添加附加组
> -d	给用户删除附加组

userdel	删除用户

> -r 用户名 	删除用户主目录,必须设置,否则用户主目录不会删除

## 用户组相关操作

groupadd	添加用户组
groupdel	删除用户组	如果用户组下面还有用户请先删除用户
usermod	修改用户组信息

> -G	设置一个附加组
> -g	修改用户组

## 远程操作

ssh连接主机
服务端安装:sudo apt-get install openssh-serve

scp远程文件操作

```shell
使用格式:  scp -r 源文件   目标文件
scp 上传 
	scp -r 本地文件  用户名@服务器IP:绝对路径 
scp下载
	scp -r  用户名@服务器IP:绝对路径  本地文件
```



##### 离线安装deb

dpkg	对deb格式软件进行安装

> -i	离线安装
> -r	卸载

##### 在线安装apt-get

> sudo apt-get install 软件包名------------>安装
> sudo apt-get remove 软件包名----------->卸载

## 更新源

略,用过太多次了不想写
apt-get 用法也有的---->更新命令.md