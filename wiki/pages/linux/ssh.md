**SSH命令**\
\
修改ssh服务的默认端口 1、查看当前服务端口\
一般ssh服务的默认端口为22端口，查看监听的端口用netstat，如下：\

```


\[root@ansiblemoniter \~\]# netstat -tnlp \|grep ssh

tcp 0 0 0.0.0.0:22 0.0.0.0:\* LISTEN 9085/sshd

tcp 0 0 :::22 :::\* LISTEN 9085/sshd


```
 2、修改默认端口\
2.1 修改配置文件\
利用修改配置文件的方法来修改ssh服务的默认端口，ssh配置文件路径如下：\

```


\[root@ansiblemoniter \~\]# ls -l /etc/ssh/sshd_config

-rw\-\-\-\-\-\-- 1 root root 3883 Dec 30 02:29 /etc/ssh/sshd_config

      未修改之前如下：

      修改之后如下：

      在开始进行修改之前，开放两个端口，一个是默认的22端口，一个是需要修改的端口，防止修改端口失败，需要进机房进行操作


```
 2.2 重启ssh服务

      重启ssh服务，使修改后的配置文件生效

2.3 查看监听端口

    查看监听端口如上所示，可以看到22端口和5309端口都进行了监听

\
\
<http://blog.csdn.net/kellyseeme/article/details/50433147>(**源地址**）
