---
title: Linux简单命令
categories: Linux
tags: linux
date: 2018-08-30 14:01:00
---

## 查看磁盘量 du
参数
> -a或-all 显示目录中个别文件的大小。
-b或-bytes 显示目录或文件大小时，以byte为单位。
-c或--total 除了显示个别目录或文件的大小外，同时也显示所有目录或文件的总和。
-k或--kilobytes 以KB(1024bytes)为单位输出。
-m或--megabytes 以MB为单位输出。
-s或--summarize 仅显示总计，只列出最后加总的值。
-h或--human-readable 以K，M，G为单位，提高信息的可读性。
-x或--one-file-xystem 以一开始处理时的文件系统为准，若遇上其它不同的文件系统目录则略过。
-L<符号链接>或--dereference<符号链接> 显示选项中所指定符号链接的源文件大小。
-S或--separate-dirs 显示个别目录的大小时，并不含其子目录的大小。
-X<文件>或--exclude-from=<文件> 在<文件>指定目录或文件。
--exclude=<目录或文件> 略过指定的目录或文件。
-D或--dereference-args 显示指定符号链接的源文件大小。
-H或--si 与-h参数相同，但是K，M，G是以1000为换算单位。
-l或--count-links 重复计算硬件链接的文件。
<!-- more -->
示例

查看当前目录中文件或目录所占空间
```
du
```
以指定单位显示，不加任何参数则为k(1k = 1024byte)， -m 兆

```
du -m
```
输出，最下面的一行是当前目录的总大小
```
2	./.openoffice/4/user
2	./.openoffice/4
2	./.openoffice
1	./.pki/nssdb
1	./.pki
1	./.ure
506	.
```
指定目录
```
du etc
```
指定多个文件, 并以兆显示
```
du file1 file2  -m
```
只显示总和的大小

```
du -s
```
## 文件权限 chmod 
chmod [cfvR] [--help] [--version] [ugoa] [+-] [rwxX][...]
> -c : 若该档案权限确实已经更改，才显示其更改动作
-f : 若该档案权限无法被更改也不要显示错误讯息
-v : 显示权限变更的详细资料
-R : 对目前目录下的所有档案与子目录进行相同的权限变更(即以递回的方式逐个变更) 
--help : 显示辅助说明
--version : 显示版本 
u 表示该档案的拥有者，g 表示与该档案的拥有者属于同一个群体(group)者，o 表示其他以外的人，a 表示这三者皆是。 
+-增加或减去权限
r 表示可读取，w 表示可写入，x 表示可执行，X 表示只有当该档案是个子目录或者该档案已经被设定过为可执行。 

示例
将 text.txt 设为所有人可读

```
chmod a+r text.txt
```
或

```
chmod ugo+r text.txt
```
将text1.txt、text2.txt设为拥有者和同一组的人可写，其他人不可写

```
chmod ug+w,o-w text1.txt text2.txt 
```
将当前目录下的所有文件及子文件设为所有人可读

```
chmod -R a+w *
```
用数字表示
```
-rw------- (600) -- 只有属主有读写权限。 
-rw-r--r-- (644) -- 只有属主有读写权限；而属组用户和其他用户只有读权限。 
-rwx------ (700) -- 只有属主有读、写、执行权限。 
-rwxr-xr-x (755) -- 属主有读、写、执行权限；而属组用户和其他用户只有读、执行权限。 
-rwx--x--x (711) -- 属主有读、写、执行权限；而属组用户和其他用户只有执行权限。 
-rw-rw-rw- (666) -- 所有用户都有文件读、写权限。这种做法不可取。 
-rwxrwxrwx (777) -- 所有用户都有读、写、执行权限。更不可取的做法。  
```

可执行文件

```
chmod -x deploy.sh

./deploy.sh
```

## 探测给定文件的类型 file
> -b：列出辨识结果时，不显示文件名称；
-c：详细显示指令执行过程，便于排错或分析程序执行的情形；
-f<名称文件>：指定名称文件，其内容有一个或多个文件名称时，让file依序辨识这些文件，格式为每列一个文件名称；
-L：直接显示符号连接所指向的文件类别；
-m<魔法数字文件>：指定魔法数字文件；
-v：显示版本信息；
-z：尝试去解读压缩文件的内容。

## 查找文件 find
> -amin<分钟>：查找在指定时间曾被存取过的文件或目录，单位以分钟计算；
-anewer<参考文件或目录>：查找其存取时间较指定文件或目录的存取时间更接近现在的文件或目录；
-atime<24小时数>：查找在指定时间曾被存取过的文件或目录，单位以24小时计算；
-cmin<分钟>：查找在指定时间之时被更改过的文件或目录；
-cnewer<参考文件或目录>查找其更改时间较指定文件或目录的更改时间更接近现在的文件或目录；
-ctime<24小时数>：查找在指定时间之时被更改的文件或目录，单位以24小时计算；
-daystart：从本日开始计算时间；
-depth：从指定目录下最深层的子目录开始查找；
-expty：寻找文件大小为0 Byte的文件，或目录下没有任何子目录或文件的空目录；
-exec<执行指令>：假设find指令的回传值为True，就执行该指令；
-false：将find指令的回传值皆设为False；
-fls<列表文件>：此参数的效果和指定“-ls”参数类似，但会把结果保存为指定的列表文件；
-follow：排除符号连接；
-fprint<列表文件>：此参数的效果和指定“-print”参数类似，但会把结果保存成指定的列表文件；
-fprint0<列表文件>：此参数的效果和指定“-print0”参数类似，但会把结果保存成指定的列表文件；
-fprintf<列表文件><输出格式>：此参数的效果和指定“-printf”参数类似，但会把结果保存成指定的列表文件；
-fstype<文件系统类型>：只寻找该文件系统类型下的文件或目录；
-gid<群组识别码>：查找符合指定之群组识别码的文件或目录；
-group<群组名称>：查找符合指定之群组名称的文件或目录；
-help或——help：在线帮助；
-ilname<范本样式>：此参数的效果和指定“-lname”参数类似，但忽略字符大小写的差别；
-iname<范本样式>：此参数的效果和指定“-name”参数类似，但忽略字符大小写的差别；
-inum<inode编号>：查找符合指定的inode编号的文件或目录；
-ipath<范本样式>：此参数的效果和指定“-path”参数类似，但忽略字符大小写的差别；
-iregex<范本样式>：此参数的效果和指定“-regexe”参数类似，但忽略字符大小写的差别；
-links<连接数目>：查找符合指定的硬连接数目的文件或目录；
-iname<范本样式>：指定字符串作为寻找符号连接的范本样式；
-ls：假设find指令的回传值为Ture，就将文件或目录名称列出到标准输出；
-maxdepth<目录层级>：设置最大目录层级；
-mindepth<目录层级>：设置最小目录层级；
-mmin<分钟>：查找在指定时间曾被更改过的文件或目录，单位以分钟计算；
-mount：此参数的效果和指定“-xdev”相同；
-mtime<24小时数>：查找在指定时间曾被更改过的文件或目录，单位以24小时计算；
-name<范本样式>：指定字符串作为寻找文件或目录的范本样式；
-newer<参考文件或目录>：查找其更改时间较指定文件或目录的更改时间更接近现在的文件或目录；
-nogroup：找出不属于本地主机群组识别码的文件或目录；
-noleaf：不去考虑目录至少需拥有两个硬连接存在；
-nouser：找出不属于本地主机用户识别码的文件或目录；
-ok<执行指令>：此参数的效果和指定“-exec”类似，但在执行指令之前会先询问用户，若回答“y”或“Y”，则放弃执行命令；
-path<范本样式>：指定字符串作为寻找目录的范本样式；
-perm<权限数值>：查找符合指定的权限数值的文件或目录；
-print：假设find指令的回传值为Ture，就将文件或目录名称列出到标准输出。格式为每列一个名称，每个名称前皆有“./”字符串；
-print0：假设find指令的回传值为Ture，就将文件或目录名称列出到标准输出。格式为全部的名称皆在同一行；
-printf<输出格式>：假设find指令的回传值为Ture，就将文件或目录名称列出到标准输出。格式可以自行指定；
-prune：不寻找字符串作为寻找文件或目录的范本样式;
-regex<范本样式>：指定字符串作为寻找文件或目录的范本样式；
-size<文件大小>：查找符合指定的文件大小的文件；
-true：将find指令的回传值皆设为True；
-typ<文件类型>：只寻找符合指定的文件类型的文件；
-uid<用户识别码>：查找符合指定的用户识别码的文件或目录；
-used<日数>：查找文件或目录被更改之后在指定时间曾被存取过的文件或目录，单位以日计算；
-user<拥有者名称>：查找符和指定的拥有者名称的文件或目录；
-version或——version：显示版本信息；
-xdev：将范围局限在先行的文件系统中；
-xtype<文件类型>：此参数的效果和指定“-type”参数类似，差别在于它针对符号连接检查。

示例
查找当前文件夹及子文件夹下的所有文件和文件夹

```
find .
```

查找 /etc下文件后缀为 **.conf** 的文件

```
find /etc -name '*.conf'
```
忽略大小写

```
find /etc -iname '*.conf'
```
查找当前文件夹及子文件夹下后缀名为 **.conf** 或 **.txt** 的文件，（**括号两边有空格哦**）
```
find . \( -name "*.conf" -o -name "*.txt" \)
```
匹配路径或文件（路径中有local或文件名含local）

```
find /usr/ -path "*local"
```
正则表达式匹配路径

```
find . -regex ".*\(\.txt\|\.pdf\)$"
```
同上，忽略大小写

```
find . -iregex ".*\(\.txt\|\.pdf\)$"
```
查询 **/etc** 下不是以 **.conf** 结尾的文件

```
find /etc ! -name "*.conf"
```
根据文件类型查找

```
find -type 类型参数
```
类型参数：
>  f 普通文件
    l 符号连接
    d 目录
    c 字符设备
    b 块设备
    s 套接字
    p Fifo

列出所有文件
```
find -type f  
```
向下最大深度限制为3

```
find -maxdepth 3 -type f
```
搜索出深度距离当前目录至少2个子目录的所有文件

```
find -mindepth -type f
```

#### 根据时间戳查找文件

 UNIX/Linux文件系统每个文件都有三种时间戳：

    访问时间（-atime/天，-amin/分钟）：用户最近一次访问时间。
    修改时间（-mtime/天，-mmin/分钟）：文件最后一次修改时间。
    变化时间（-ctime/天，-cmin/分钟）：文件数据元（例如权限等）最后一次修改时间。

查找7天内修改过的文件

```
find -type f -atime -7
```
修改时间正好是7天的文件

```
find -type f -atime 7
```

查找修改时间大于7天的所有文件

```
find -type f atime +7
```

查找访问时间在60分钟以内的文件

```
find -type f -amin -60
```
#### 根据文件大小匹配

```
find . -type f size 文件大小
```
 文件大小单元：

    b —— 块（512字节）
    c —— 字节
    w —— 字（2字节）
    k —— 千字节
    M —— 兆字节
    G —— 吉字节

搜索大于10k的所有文件

```
find -type f -size 10k
```

#### 删除匹配文件

```
find -type f -name '*.txt' -delete
```
#### 根据文件权限/所有权匹配

```
find -type f -perm 777
```
找出当前目录下权限 **不是** 644的sh文件
```
find -type f  -name '*.sh' ! -perm 644
```
找出当前目录用户root拥有的所有文件

```
find . -type f -user root
```
找出当前目录用户组sunk拥有的所有文件

```
find . -type f -group sunk
```

## 过滤 grep
过滤出 /etc/passwd 文件中包含 root 的记录
```
grep 'root' /etc/passwd
```
递归地过滤出 /var/log/ 目录中包含 linux 的记录

```
grep -r 'linux' /var/log/
```
## 管道 |
> 简单来说, Linux 中管道的作用是将上一个命令的输出作为下一个命令的输入, 像 pipe 一样将各个命令串联起来执行, 管道的操作符是 |

比如, 我们可以将 cat 和 grep 两个命令用管道组合在一起

```
cat /etc/passwd | grep 'root'
```
过滤出 /etc 目录中名字包含 ssh 的目录(不包括子目录)

```
ls /etc | grep 'ssh'
```

### 重定向 > <
> 可以使用 > 或 < 将命令的输出重定向到一个文件中

```
echo 'Hello World' > ~/test.txt
```

## 运维常用命令
### ping
对 cloud.tencent.com 发送 4 个 ping 包, 检查与其是否联通
```
ping -c 4 www.baidu.com
```
### netstat 命令
> netstat 命令用于显示各种网络相关信息，如网络连接, 路由表, 接口状态等等

列出所有处于监听状态的tcp端口

```
netstat -lt
```
查看所有的端口信息, 包括 PID 和进程名称

```
netstat -tulpn
```

