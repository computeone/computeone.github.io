**lsof简介**\
lsof（list open
files）是一个列出当前系统打开文件的工具。在linux环境下，任何事物都以文件的形式存在，通过文件不仅仅可以访问常规数据，还可以访问网络连接和硬件。所以如传输控制协议
(TCP) 和用户数据报协议 (UDP)
套接字等，系统在后台都为该应用程序分配了一个文件描述符，无论这个文件的本质如何，该文件描述符为应用程序与基础操作系统之间的交互提供了通用接口。因为应用程序打开文件的描述符列表提供了大量关于这个应用程序本身的信息，因此通过lsof工具能够查看这个列表对系统监测以及排错将是很有帮助的。
lsof使用\
\
lsof输出信息含义\
在终端下输入lsof即可显示系统打开的文件，因为 lsof
需要访问核心内存和各种文件，所以必须以 root
用户的身份运行它才能够充分地发挥其功能。\

```
 COMMAND PID USER FD TYPE DEVICE SIZE NODE NAME init 1 root cwd
DIR 3,3 1024 2 / init 1 root rtd DIR 3,3 1024 2 / init 1 root txt REG
3,3 38432 1763452 /sbin/init init 1 root mem REG 3,3 106114 1091620
/lib/libdl-2.6.so init 1 root mem REG 3,3 7560696 1091614
/lib/libc-2.6.so init 1 root mem REG 3,3 79460 1091669
/lib/libselinux.so.1 init 1 root mem REG 3,3 223280 1091668
/lib/libsepol.so.1 init 1 root mem REG 3,3 564136 1091607 /lib/ld-2.6.so
init 1 root 10u FIFO 0,15 1309 /dev/initctl


```
 例如： 查看22端口现在运行的情况\

```


\# lsof -i :22 COMMAND PID USER FD TYPE DEVICE SIZE NODE NAME sshd 1409
root 3u IPv6 5678 TCP \*:ssh (LISTEN)


```


一、查找谁在使用文件系统\
在卸载文件系统时，如果该文件系统中有任何打开的文件，操作通常将会失败。那么通过lsof可以找出那些进程在使用当前要卸载的文件系统，如下：\

```


\# lsof /GTES11/ COMMAND PID USER FD TYPE DEVICE SIZE NODE NAME bash
4208 root cwd DIR 3,1 4096 2 /GTES11/ vim 4230 root cwd DIR 3,1 4096 2
/GTES11/


```

