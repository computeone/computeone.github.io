**find命令**\
\
**1. List all files in current and sub directories**\
This command lists out all the files in the current directory as well as
the subdirectories in the current directory.\
\

```
 \$ find . ./abc.txt ./subdir ./subdir/how.php ./cool.php

```
 The command is same as the following\

```
 \$ find . \$ find . -print 
```
 **2. Search specific
directory or path**\
The following command will look for files in the test directory in the
current directory. Lists out all files by default.\
\

```
 \$ find ./test ./test ./test/abc.txt ./test/subdir
./test/subdir/how.php ./test/cool.php


```
 The following command searches for files by their name.\
\

```
 \$ find ./test -name \"abc.txt\" ./test/abc.txt


```
 We can also use wildcards\

```


\$ find ./test -name \"\*.php\" ./test/subdir/how.php ./test/cool.php


```
 Note that all sub directories are searched recursively. So
this is a very powerful way to find all files of a given extension.\
\
**Ignore the case**\
It is often useful to ignore the case when searching for file names. To
ignore the case, just use the \"iname\" option instead of the \"name\"
option.\
\

```
 \$ find ./test -iname \"\*.Php\" ./test/subdir/how.php
./test/cool.php


```
 **3. Limit depth of directory traversal**\
The find command by default travels down the entire directory tree
recursively, which is time and resource consuming. However the depth of
directory travesal can be specified. For example we don\'t want to go
more than 2 or 3 levels down in the sub directories. This is done using
the maxdepth option.\

```


\$ find ./test -maxdepth 2 -name \"\*.php\" ./test/subdir/how.php
./test/cool.php


```
 
```


\$ find ./test -maxdepth 1 -name \*.php ./test/cool.php


```
 The second example uses maxdepth of 1, which means it will not
go lower than 1 level deep, either only in the current directory.\
\
This is very useful when we want to do a limited search only in the
current directory or max 1 level deep sub directories and not the entire
directory tree which would take more time.\
\
Just like maxdepth there is an option called mindepth which does what
the name suggests, that is, it will go atleast N level deep before
searching for the files.\
\
**4. Invert match**\
It is also possible to search for files that do no match a given name or
pattern. This is helpful when we know which files to exclude from the
search.\
\

```
 \$ find ./test -not -name \"\*.php\" ./test ./test/abc.txt
./test/subdir


```
 So in the above example we found all files that do not have
the extension of php, either non-php files. The find command also
supports the exclamation mark inplace of not.\
\
\
<http://www.binarytides.com/linux-find-command-examples/>
