[TOC]

# 1 Discovering the file system

## 1.1 Filesystem, history, FSSTND, /bin, /sbin, /home, /root, /etc, /lib, /tmp, /var, /usr, /dev

Remember that not so long ago, programs and data used to be stored on punch cards.



You can imagine that the abilities to store programs on disk drives revolutionized the world of programming.



 For the user, a file system is best visualized as a tree.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200412145019771.png" alt="image-20200412145019771" style="zoom:50%;" />




Files are grouped into directories, or folders-- a concept used by most operating systems.

These directories contain further files and/or other directories.

So there's a root directory and then a number of subdirectories.

Such an organization generates a hierarchy of directories and files organized into a tree.

REMI : On Unix/Linux, the root of the file system is denoted slash.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200412145247513.png" alt="image-20200412145247513" style="zoom:33%;" />

The root folder would, therefore, be slash. A folder and a subfolder will be denoted slash folder slash subfolder.

A file in that subfolder will be denoted slash folder slash subfolder slash file.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200412145339742.png" alt="image-20200412145339742" style="zoom:33%;" />

How do we organize the hierarchy of directories and files?

From the user's point of view, well, it's up to them to decide how to organize their own files and folders.
REMI : The operating system itself has lots of files to keep track of, as well -- utility programs, applications, methods to communicate with devices, et cetera.

In August 1993, the process of standardizing the file system hierarchy began.

**FSSTND**, Filesystem Standard, is a standard specific to the Filesystem hierarchy to GNU Linux.

The vast majority of GNU Linux distributions do not strictly follow this standardization format.

We're going to give you some directory names that can be found in the vast majority of Linux distributions.



### 1.1.1 /bin

This is the directory which contains all of the basic commands needed to start and use a minimal system.
The directory name is derived from the abbreviation of **binary**.

The executable file of an application is called a binary.



### 1.1.2 /sbin

This directory contains commands-- executable, so binaries-- for the super user, also called root user.

The root user is the administrator of the computer and has more powers than simple users.

Superpowers, I would say.



### 1.1.13 /home

Home contains all of user directories-- for example, /home/smith or /home/remi for me.



### 1.1.4 /root

This is the home directory of the root user, the user that has the superpowers.



### 1.1.5 /etc.

This directory contains configuration files.

In fact, it is the abbreviation of **Editable Text Configuration**.



### 1.1.6 /lib

Here, the system stores software libraries required for executables in /bin and /sbin



### 1.1.7 /tmp

This directory is for temporary files.

Sometimes, it is located in /var/tmp or /run/tmp

It is usually emptied every time you restart the computer.

So be careful.

When you use this folder and restart your computer, everything will be destroyed inside.



### 1.1.8 /var

This contains various files used by the operating system, such as databases, email boxes, and history.

A log of what happened on the system is in /var/logs, for example.



### 1.1.9 /usr

USR is the acronym of **Unix System Resources**, and not user, as one might think.

This folder contains some subfolders, similar to those present that the roots, but they are used to extend the system operations.

For example, this folder includes **/usr/bin**

That contains executable binaries that are not already present in /bin and, therefore, not essential to a minimal system.

Or **/usr/lib** that contains those libraries that are not essential for a minimal system.



### 1.1.10 /dev

This directory contains files, each of which corresponds, directly or indirectly, to a physical device.

dev is a decent abbreviation for device. This is one of the strengths of Linux.

It considers everything as a file, including devices, such as /dev/printer, /dev/audio, /dev/mem for memory, /dev/networkcard, and so forth.



## 1.2 pwd, cd, ls, absolute path, relative path (1)



### 1.2.1 pwd

It means print working directory.

It is the directory in which you are working just now.

So anyway, pwd is to print the working directory.



### 1.2.2 ls

Let's try now to list the files and folders, directories inside the working directory.



### 1.2.3 cd

cd stands for **change directory**.



#### 1.2.3.1 cd + (without anything)

So let's go to the **home directory**.



#### 1.2.3.2 cd /

So let's go to the **root directory**.

```
[chenjj@node100 ~]$ cd /
[chenjj@node100 /]$ pwd
/
[chenjj@node100 /]$ ls
bin   clusconf_log-.out  etc   lib    lost+found  mnt  proc    root  sbin  srv  tmp  var
boot  dev                home  lib64  media       opt  public  run   soft  sys  usr
```



### 1.2.4 cd /bin

```
cd /bin
ls
[		csh		echo		ksh		mkdir		rm		sync		zsh
bash		dash		ed		launchctl	mv		rmdir		tcsh
cat		date		expr		link		pax		sh		test
chmod		dd		hostname	ln		ps		sleep		unlink
cp		df		kill		ls		pwd		stty		wait4path
```





### 1.2.4 cd /sys


ls

And oh, we have other directories : block, class, devices, et cetera, et cetera.



### 1.2.5 ls

#### 1.2.5.1 ls -a

And this will list the files and also the hidden files.
And the names of the hidden files are starting with a dot.

So we have files and folders also.



#### 1.2.5.2 ls -al
查看所有文件（包括隐藏文件） 的大小、日期等详细信息。



#### 1.2.5.3 ll
查看所有非隐藏文件的大小、日期等详细信息。




### 1.2.6 dot and dot dot

dot (.) is the current directory. 
dot dot  (..) is the parent directory.

So if I type cd .. then it will go to the parent directory of my home directory, which is /home, indeed as you can see here.

And if I go back again to cd .. then we are back to the root directory, which is the parent of /home, indeed.

Let's go back to the home directory.

And this time, I can do something like this with the relative paths ../.. And it means the parent of the parent of this directory. And it will go to the root directory, indeed. If I pwd, it's the root directory.

All right, let's go now to a directory, for example, sys.

As you can see here, we have ./ so it's a **relative path**.

And then in the parent, I know that I have  home and I have in home user. So here, I used a relative path to go back to the home folder.
And did it work?
It worked because I am in /home/user. Let's go back to /sys

All right, and this time, let's try to write directly the **absolute path**. Because it is absolute, you only have to start from the /and to know the path from the beginning.



## 1.3 pwd, cd, ls, absolute path, relative path (2)

### 1.3.1 get the type of a file

file [file name]就可以知道文件类型了



### 1.3.2 a common way to see the path of a file

which [file/application/command]

可以得知绝对路径

```
[chenjj@node100 ~]$ which realpath
/usr/bin/realpath
```


```
[chenjj@node100 ~]$ realpath cat
/public/home/jlyang/chenjj/cat
[chenjj@node100 ~]$ which cat
/usr/bin/cat
```



```
which which
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
	/usr/bin/alias
	/usr/bin/which
```



### 1.3.3 cat

Let's try which cat.

cat is, indeed, installed in /bin/cat.

```
[chenjj@node100 ~]$ which cat
/usr/bin/cat
```



### 1.3.4 file

```
[chenjj@node100 ~]$ which file
/usr/bin/file
```



### 1.3.5 nano

nana [file name]

可以新建一个名为file name的nano文本



# 2 Creating and deleting files and folders

## 2.1 Touch, rm, names with spaces

### 2.1.1 vi file

新建名字为”file“的vi文件

输入任意文本，如：program C

保存文件并退出：```:wq```



### 2.1.2 rm file

删除file文件



### 2.1.3 文件名不能有空格

如果有一个空格，那么就会生成2个文件



### 2.1.4 ls -l

比普通的ls，得到更多信息



## 2.2 cat less

### 2.2.1 echo "hello world" > file.txt

将hello world写入文件file.txt



### 2.2.2 cat file.txt

输出：

```
hello world
```



### 2.2.3 cat file.txt > file2.txt

这个操作类似copy。



cat file2.txt

输出：

```
hello world
```





### 2.2.4 cat > file3.txt

回车后，等待人继续输入东西

输入”this is file3." 

通过“control + D”退出。

则file3.txt的内容是```this is file3.```



## 2.4 mkdir, rm -r

### 2.4.1 mkdir

=make director，新建文件夹



### 2.4.2 rm -r

删除文件夹



# 3 Unblocking yourself in the command line

## 3.1 Unblock yourself in the command line

### 3.1.1 退出vim

先esc，再输入：```:q```

如果是```:q!```，则强制退出后vim，不保存。



### 3.1.2 退出prompt的文本编辑

如 cat > file.txt

control + D



### 3.1.3 退出正在运行的一个小程序

control + C



# 4 Modifying, moving and copying files and folders

## 4.1 mv: rename and move

mv a1 a2

将a1重命名为a2

a1和a2前都可以加地址，即可实现移动文件

mv可用于文件和文件夹



## 4.2 cp, cp -r

cp，意味着copy。

cp针对文件，cp -r针对文件夹



# 5 Searching files and folders

## 5.1 Find locate

### 5.1.1 echo

```
[chenjj@admin ~]$ echo 8*
8-7-1-3.pbs 8-experiment-Perovskite
```

打印目录中的文件和文件夹



### 5.1.2 find

#### 5.1.2.1 find 

```
[chenjj@admin ~]$ find *.pbs
8-7-1-3.pbs
```



#### 5.1.2.2 find /

```find /```，则会刷出在/内的所有文件，直到内存不够才会停止



#### 5.1.2.3 find .

列出当前目录及子目录下的所有文件



 #### 5.1.2.4 find . -name f1.txt

列出当前目录及子目录下，名字为f1.txt的所有文件。



#### 5.1.2.5 find . -name f1*

列出当前目录及子目录下，名字以f1开头的所有文件。

.可以换成任意目录

*可以放在f1前，也可以放在f1后，也可以前后都有：\*f1\*



#### 5.1.2.6 find . -name f1* > a1.txt

结果写进了a1.txt中：

```
[chenjj@admin ~]$ cat a1.txt 
./f1.txt
```

