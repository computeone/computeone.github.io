
```
 git config \[\<file-option\>\] \[type\] \[\--show-origin\]
\[-z\|\--null\] name \[value \[value_regex\]\] git config
\[\<file-option\>\] \[type\] \--add name value git config
\[\<file-option\>\] \[type\] \--replace-all name value \[value_regex\]
git config \[\<file-option\>\] \[type\] \[\--show-origin\]
\[-z\|\--null\] \--get name \[value_regex\] git config
\[\<file-option\>\] \[type\] \[\--show-origin\] \[-z\|\--null\]
\--get-all name \[value_regex\] git config \[\<file-option\>\] \[type\]
\[\--show-origin\] \[-z\|\--null\] \[\--name-only\] \--get-regexp
name_regex \[value_regex\] git config \[\<file-option\>\] \[type\]
\[-z\|\--null\] \--get-urlmatch name URL git config \[\<file-option\>\]
\--unset name \[value_regex\] git config \[\<file-option\>\]
\--unset-all name \[value_regex\] git config \[\<file-option\>\]
\--rename-section old_name new_name git config \[\<file-option\>\]
\--remove-section name git config \[\<file-option\>\] \[\--show-origin\]
\[-z\|\--null\] \[\--name-only\] -l \| \--list git config
\[\<file-option\>\] \--get-color name \[default\] git config
\[\<file-option\>\] \--get-colorbool name \[stdout-is-tty\] git config
\[\<file-option\>\] -e \| \--edit


```



```
 \$ git config \--global user.name \"John Doe\" \$ git config
\--global user.email johndoe@example.com 
```


**Adding a remote**\
To add a new remote, use the git remote add command on the terminal, in
the directory your repository is stored at.\
The git remote add command takes two arguments:\

1.  A remote name, for example, origin\
    - A remote URL, for example, <https://github.com/user/repo.git>

**For example**:\

```
 git remote add origin\'\'
<https://github.com/user/repo.git>\'\' \# Set a new remote

git remote -v \# Verify new remote origin
<https://github.com/user/repo.git> (fetch) origin
<https://github.com/user/repo.git> (push) 
```
\
**二、git reset的用法** 
```
 从上图可知：git reset \-- files
用来撤销最后一次的git add files（因为每git add
file一次，暂存区的文件都会被更改一次），你也可以用git reset
撤销所有暂存区域文件。 另外： 一、git reset的用法：git reset + commit号
1、git
reset命令后面需要加2种参数：\"\--hard\"和\"\--soft\"，如果不加，默认情况下是\"\--soft\"。\
2、\--soft表示该条commit号之后（时间作为参考点）的所有commit的修改都会退回到git缓冲区中。所以使用git
status命令可以在缓冲区中看到这些修改。
3、\"\--hard\"则表示缓冲区中不会存储这些修改，git会直接丢弃这部分内容，但需要注意的一个问题是：这样的重置是直接在本地的修改，无法提交到远程服务器，如果直接丢弃的内容已经被推到远程服务器上了，则会造成本地和服务器无法同步的问题，即git
reset
\--hard只能针对本地操作，不能针对远程服务器进行同样操作。如果从本地删掉的内容没有推到服务器上，则不会有副作用，如果被推到服务器，则下次本地和服务器进行同步时，这\
部分删掉的内容仍然会回来。\
（其实这个问题则可以很好的被git revert 命令解决，使用git revert +
commit号，该命令撤销对某个commit的提交，这一撤销动作会作为一个新的修改存储起来，这样，当你和服务器同步时，就不会产生什么副作用。）
其实在merge的时候，也有可能会用到git reset. 如果我们当前使用git
pull的时候，可能会出现merge冲突，在冲突状态下，需要解决冲突的文件会从index暂存区打回到工作区。
如果有冲突的时候，一般用如下步骤解决冲突： 1、用工具或者手工解决冲突
2、git add 命令来表明冲突已经解决。 3、再次commit已解决冲突的文件。
这当中，可以使用git reset \--hard ORIG_HEAD用来撤销已经commit的merge.
使用git reset \--hard HEAD 用来撤销还没commit
的merge,其实原理就是放弃index和工作区的改动。 也可以使用git reset
\--merge ORIG_HEAD，注意其中的\--hard 换成了
\--merge，这样就可以避免在回滚时清除working tree。


```

