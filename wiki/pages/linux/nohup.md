**nohup命令**\
\
**nohup** is a POSIX command to ignore the HUP (hangup) signal. The HUP
signal is, by convention, the way a terminal warns dependent processes
of logout.\
\
Output that would normally go to the terminal goes to a file called
nohup.out if it has not already been redirected.\

```


nohup ./program \>/dev/null 2\>log &

nohup ./program \>/dev/null 2\>&1 &


```
\
1. 基本概念

    a、I/O重定向通常与 FD有关，shell的FD通常为10个，即 0～9；（FD：file descripter，文件描述符）
    b、常用FD有3个，为: 0（stdin，标准输入）、1（stdout，标准输出）、2（stderr，标准错误输出），默认与keyboard、monitor、monitor有关；
    c、用 < 来改变读进的数据信道(stdin)，使之从指定的档案读进；
    d、用 > 来改变送出的数据信道(stdout, stderr)，使之输出到指定的档案；
    e、0 是 < 的默认值，因此 < 与 0<是一样的；同理，> 与 1> 是一样的；
    f、在IO重定向 中，stdout 与 stderr 的管道会先准备好，才会从 stdin 读进资料；
    g、管道“|”(pipe line):上一个命令的 stdout 接到下一个命令的 stdin;
    h、tee 命令是在不影响原本 I/O 的情况下，将 stdout 复制一份到档案去;
    i、bash（ksh）执行命令的过程：分析命令－变量求值－命令替代（``和$( )）－重定向－通配符展开－确定路径－执行命令；
    j、( )  将 command group 置于 sub-shell 去执行，也称 nested sub-shell，它有一点非常重要的特性是：继承父shell的Standard input, output, and error plus any other open file descriptors。
    k、exec 命令：常用来替代当前 shell 并重新启动一个 shell，换句话说，并没有启动子 shell。使用这一命令时任何现有环境都将会被清除，。exec 在对文件描述符进行操作的时候，也只有在这时，exec 不会覆盖你当前的 shell 环境。

2\. 基本IO 
```


    cmd > file                        把 stdout 重定向到 file 文件中
    cmd >> file                        把 stdout 重定向到 file 文件中(追加)
    cmd 1> fiel                        把 stdout 重定向到 file 文件中
    cmd > file 2>&1                把 stdout 和 stderr 一起重定向到 file 文件中
    cmd 2> file                        把 stderr 重定向到 file 文件中
    cmd 2>> file                        把 stderr 重定向到 file 文件中(追加)
    cmd >> file 2>&1                把 stderr 和 stderr 一起重定向到 file 文件中
    cmd < file >file2                cmd 命令以 file 文件作为 stdin，以 file2 文件作为 stdout
    cat <>file                             以读写的方式打开 file
    cmd < file                        cmd 命令以 file 文件作为 stdin
    cmd << delimiter                Here document，从 stdin 中读入，直至遇到delimiter 分界符


```


    \\
    \\
    http://blog.csdn.net/qinglu000/article/details/18963031
