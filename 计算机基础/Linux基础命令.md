# `Linux基础命令`

`快捷键：Tab命令和文件名补全；`

`Ctrl+C中断正在运行的程序`

Ctrl+D结束键盘输入

```
--help 指令的基本用法和选项介绍
```

```
man是manual的缩写，将指令的具体信息显示出来
```

```
info 将文档分成一个一个页面，诶个页面可以跳转
```

`who`

`在关机前需要先使用who命令查看有没有其它用户在线`

`shutdown关机命令`

```mysql
## shutdown [-krhc] 时间 [信息]
-k ： 不会关机，只是发送警告信息，通知所有在线的用户
-r ： 将系统的服务停掉后就重新启动
-h ： 将系统的服务停掉后就立即关机
-c ： 取消已经在进行的 shutdown
```



`sudo允许一般用户使用root权限执行命令`

### `包管理工具`

`包管理工具RPM和DPKG，我一般用的RPM的会比较多`

### `VIM`

`编辑文件命令，在进入该文件后，可以用i或者a\o进行编辑文档，/搜索相关内容。：后用户保存退出等操作，：wq,保存并退出，：w保存，：w!当文件只读后，强制写入文件，：q离开，：q!强制退出（不保存），:wq！强制保存后退出`

```
ls 
ls-l
列出当前当前文件夹的全部文件

cd 
切换目录

mkdir
创建目录

rmdir
删除目录

touch
创建文件

cp
复制文件
cp 文件名 新的文件名 /存放路径

rm 
删除文件

mv 
移动文件

cat
查看文件内容

more
less
翻页

head
获取文件前几行

which
指令搜索

whereis
文件搜索

find
文件搜索


```

```
修改权限
chmod ugoa +-= rwx filename
 u：拥有者
- g：所属群组
- o：其他人
- a：所有人
- +：添加权限
- -：移除权限
- =：设定权限
r 读
w 写
x执行权限
```

`压缩解压`

```
gzip -cdtv# filename
-c ：将压缩的数据输出到屏幕上
-d ：解压缩
-t ：检验压缩文件是否出错
-v ：显示压缩比等信息
-# ： # 为数字的意思，代表压缩等级，数字越大压缩比越高，默认为 6

打包
tar -zjJ cv(tv)(xv) -f 已有的文件
-z ：使用 zip；
-j ：使用 bzip2；
-J ：使用 xz；
-c ：新建打包文件；
-t ：查看打包文件里面有哪些文件；
-x ：解打包或解压缩的功能；
-v ：在压缩/解压缩的过程中，显示正在处理的文件名；
-f : filename：要处理的文件；
-C 目录 ： 在特定目录解压缩。
```

```
lsof -i:80 查看端口占用情况
PS -l 查看进程
PS aux |grep 查看特定经常
top 查看系统运行情况相当于程序管理器，显示进程信息
netstat -anp|grep 80查看特定端口
systemctl start sevice
systemctl stop service
systemctl status service
./serv
```

