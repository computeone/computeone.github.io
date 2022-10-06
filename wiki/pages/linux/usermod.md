**USERMODE命令**\
\
**usermod命令**用于修改用户的基本信息。usermod命令不允许你改变正在线上的使用者帐号名称。当usermod命令用来改变user
id，必须确认这名user没在电脑上执行任何程序。你需手动更改使用者的crontab档。也需手动更改使用者的at工作档。采用NIS
server须在server上更动相关的NIS设定。\
\
**语法**\

```


usermod(选项)(参数) 选项 -c\<备注\>：修改用户帐号的备注文字；
-d\<登入目录\>：修改用户登入时的目录；
-e\<有效期限\>：修改帐号的有效期限；
-f\<缓冲天数\>：修改在密码过期后多少天即关闭该帐号；
-g\<群组\>：修改用户所属的群组； -G\<群组\>；修改用户所属的附加群组；
-l\<帐号名称\>：修改用户帐号名称； -L：锁定用户密码，使密码无效；
-s：修改用户登入后所使用的shell； -u：修改用户ID； -U:解除密码锁定。


```
 **参数**\
登录名：指定要修改信息的用户登录名。\
\*\* 实例\*\*\
将newuser2添加到组staff中： 
```


usermod -G staff newuser2


```
 **用户（user）和用户组（group）相关的配置文件、命令或目录；**\
\

```


1、与用户（user）和用户组（group）相关的配置文件；

1）与用户（user）相关的配置文件； /etc/passwd
注：用户（user）的配置文件； /etc/shadow 注：用户（user）影子口令文件；

2）与用户组（group）相关的配置文件； /etc/group
注：用户组（group）配置文件； /etc/gshadow
注：用户组（group）的影子文件；

在/etc/group 中的每条记录分四个字段： 第一字段：用户组名称；
第二字段：用户组密码； 第三字段：GID
第四字段：用户列表，每个用户之间用,号分割；本字段可以为空；如果字段为空表示用户组为GID的用户名

1）管理用户（user）的工具或命令； useradd 注：添加用户 adduser
注：添加用户 passwd 注：为用户设置密码 usermod
注：修改用户命令，可以通过usermod 来修改登录名、用户的家目录等等； pwcov
注：同步用户从/etc/passwd 到/etc/shadow pwck
注：pwck是校验用户配置文件/etc/passwd 和/etc/shadow
文件内容是否合法或完整； pwunconv 注：是pwcov
的立逆向操作，是从/etc/shadow和 /etc/passwd 创建/etc/passwd ，然后会删除
/etc/shadow 文件；

2）管理用户组（group）的工具或命令； groupadd 注：添加用户组； groupdel
注：删除用户组； groupmod 注：修改用户组信息 
```

