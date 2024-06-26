top命令是Linux下常用的性能分析工具，能够实时显示系统中各个进程的资源占用状况，类似于Windows的任务管理器。下面详细介绍它的使用方法。top是一个动态显示过程,即可以通过用户按键来不断刷新当前状态.如果在前台执行该命令,它将独占前台,直到用户终止该程序为止.比较准确的说,top命令提供了实时的对系统处理器的状态监视.它将显示系统中CPU最"敏感"的任务列表.该命令可以按CPU使用.内存使用和执行时间对任务进行排序；而且该命令的很多特性都可以通过交互式命令或者在个人定制文件中进行设定.\

```
 1．命令格式： top \[参数\] 2．命令功能：
显示当前系统正在执行的进程的相关信息，包括进程ID、内存占用率、CPU占用率等
3．命令参数： -b 批处理 -c 显示完整的治命令 -I 忽略失效过程 -s 保密模式
-S 累积模式 -i\<时间\> 设置间隔时间 -u\<用户名\> 指定用户名 -p\<进程号\>
指定进程 -n\<次数\> 循环显示的次数 
```
 **4．使用实例**：\
实例1：显示进程信息\
命令：\
top\
输出：\
\[root@TG1704 log\]# top top - 14:06:23 up 70 days, 16:44, 2 users, load
average: 1.25, 1.32, 1.35 Tasks: 206 total, 1 running, 205 sleeping, 0
stopped, 0 zombie Cpu(s): 5.9%us, 3.4%sy, 0.0%ni, 90.4%id, 0.0%wa,
0.0%hi, 0.2%si, 0.0%st Mem: 32949016k total, 14411180k used, 18537836k
free, 169884k buffers Swap: 32764556k total, 0k used, 32764556k free,
3612636k cached

    PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND                                                                

28894 root 22 0 1501m 405m 10m S 52.2 1.3 2534:16 java 18249 root 18 0
3201m 1.9g 11m S 35.9 6.0 569:39.41 java 2808 root 25 0 3333m 1.0g 11m S
24.3 3.1 526:51.85 java 25668 root 23 0 3180m 704m 11m S 14.0 2.2
360:44.53 java

    574 root      25   0 3168m 611m  10m S 12.6  1.9 556:59.63 java                                                                   

1599 root 20 0 3237m 1.9g 11m S 12.3 6.2 262:01.14 java 1008 root 21 0
3147m 842m 10m S 0.3 2.6 4:31.08 java 13823 root 23 0 3031m 2.1g 10m S
0.3 6.8 176:57.34 java 28218 root 15 0 12760 1168 808 R 0.3 0.0 0:01.43
top 29062 root 20 0 1241m 227m 10m S 0.3 0.7 2:07.32 java

      1 root      15   0 10368  684  572 S  0.0  0.0   1:30.85 init                                                                   
      2 root      RT  -5     0    0    0 S  0.0  0.0   0:01.01 migration/0                                                            
      3 root      34  19     0    0    0 S  0.0  0.0   0:00.00 ksoftirqd/0                                                            
      4 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/0                                                             
      5 root      RT  -5     0    0    0 S  0.0  0.0   0:00.80 migration/1                                                            
      6 root      34  19     0    0    0 S  0.0  0.0   0:00.00 ksoftirqd/1                                                            
      7 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/1                                                             
      8 root      RT  -5     0    0    0 S  0.0  0.0   0:20.59 migration/2                                                            
      9 root      34  19     0    0    0 S  0.0  0.0   0:00.09 ksoftirqd/2                                                            
     10 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/2                                                             
     11 root      RT  -5     0    0    0 S  0.0  0.0   0:23.66 migration/3                                                            
     12 root      34  19     0    0    0 S  0.0  0.0   0:00.03 ksoftirqd/3                                                            
     13 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/3                                                             
     14 root      RT  -5     0    0    0 S  0.0  0.0   0:20.29 migration/4                                                            
     15 root      34  19     0    0    0 S  0.0  0.0   0:00.07 ksoftirqd/4                                                            
     16 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/4                                                             
     17 root      RT  -5     0    0    0 S  0.0  0.0   0:23.07 migration/5                                                            
     18 root      34  19     0    0    0 S  0.0  0.0   0:00.07 ksoftirqd/5                                                            
     19 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/5                                                             
     20 root      RT  -5     0    0    0 S  0.0  0.0   0:17.16 migration/6                                                            
     21 root      34  19     0    0    0 S  0.0  0.0   0:00.05 ksoftirqd/6                                                            
     22 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/6                                                             
     23 root      RT  -5     0    0    0 S  0.0  0.0   0:58.28 migration/7


```
 说明： 统计信息区：
前五行是当前系统情况整体的统计信息区。下面我们看每一行信息的具体意义。
第一行，任务队列信息，同 uptime 命令的执行结果，具体参数说明情况如下：
14:06:23 --- 当前系统时间 up 70 days, 16:44 ---
系统已经运行了70天16小时44分钟（在这期间系统没有重启过的吆！） 2 users
--- 当前有2个用户登录系统 load average: 1.15, 1.42, 1.44 --- load
average后面的三个数分别是1分钟、5分钟、15分钟的负载情况。 load
average数据是每隔5秒钟检查一次活跃的进程数，然后按特定算法计算出的数值。如果这个数除以逻辑CPU的数量，结果高于5的时候就表明系统在超负荷运转了。
第二行，Tasks --- 任务（进程），具体信息说明如下：
系统现在共有206个进程，其中处于运行中的有1个，205个在休眠（sleep），stoped状态的有0个，zombie状态（僵尸）的有0个。
第三行，cpu状态信息，具体属性说明如下： 5.9%us ---
用户空间占用CPU的百分比。 3.4% sy --- 内核空间占用CPU的百分比。 0.0% ni
--- 改变过优先级的进程占用CPU的百分比 90.4% id --- 空闲CPU百分比 0.0% wa
--- IO等待占用CPU的百分比 0.0% hi --- 硬中断（Hardware
IRQ）占用CPU的百分比 0.2% si --- 软中断（Software
Interrupts）占用CPU的百分比
备注：在这里CPU的使用比率和windows概念不同，需要理解linux系统用户空间和内核空间的相关知识！
第四行,内存状态，具体信息如下： 32949016k total --- 物理内存总量（32GB）
14411180k used --- 使用中的内存总量（14GB） 18537836k free ---
空闲内存总量（18GB） 169884k buffers --- 缓存的内存量 （169M）
第五行，swap交换分区信息，具体信息说明如下： 32764556k total ---
交换区总量（32GB） 0k used --- 使用的交换区总量（0K） 32764556k free ---
空闲交换区总量（32GB） 3612636k cached --- 缓冲的交换区总量（3.6GB）

```

