[TOC]

# 1 Compiling C programs under Linux

## 1.1 Difference between interpreter and compiler

### 1.1.1 interpreter

将你的表达转换成机器语言，这个过程很快；

但机器执行时，需要一个一个来，速度慢；

你看见结果，来得及纠错。

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200422220000206.png" alt="image-20200422220000206" style="zoom:33%;" />

### 1.1.2 compiler

你直接交给机器，这个过程比较慢，因为对方需要时间理解；

但开始执行时，速度很快；

如果有错，是来不及纠错的，而是会立刻出问题。

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200422220032619.png" alt="image-20200422220032619" style="zoom:33%;" />



### 1.1.3 对比

1. interpreter

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200422220138388.png" alt="image-20200422220138388" style="zoom:33%;" />

一行行执行任务：

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200422220400176.png" alt="image-20200422220400176" style="zoom:33%;" />



2. compiler

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200422220239066.png" alt="image-20200422220239066" style="zoom:33%;" />



任务一起执行

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200422220333296.png" alt="image-20200422220333296" style="zoom:33%;" />

## 1.2 Compile a C program automatically on Weblinux

GCC, namely Gnu C compiler

gcc，将hello.c生成可执行程序hello，然后执行程序hello

```c
\\hello.c
#include <stdio.h>

int main(){
    printf("Hello world!\n");
    return 0;
}
```



## 1.3 Compile a C program using GCC

### 1.3.1 直接用gcc，生成a.out

```
[chenjj@node100 10-C_program]$ gcc hello.c 
[chenjj@node100 10-C_program]$ ls
a.out  hello.c
```



a.out是可执行程序。

处理器是64-bit的。

```
[chenjj@node100 10-C_program]$ file a.out 
a.out: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.32, BuildID[sha1]=6b02e7eb279bebe9753229701b9f061c5abb8669, not stripped
```



### 1.3.2 执行a.out

```
[chenjj@node100 10-C_program]$ ./a.out 
Hello world!
```



### 1.3.3 用-o，指定可执行程序的名字

```
[chenjj@node100 10-C_program]$ gcc hello.c -o hello
[chenjj@node100 10-C_program]$ ./hello 
Hello world!
```



### 1.3.4 gcc的其他设定

1. -std

-std=c11，即gcc这个compiler是2011版本的



2. -W

It means that we don't want to have all of the warnings, so possible warnings are possible mistakes that you made in the program, and we want to have all of them printed.



3. -fmax-errors=10

that means that you will have a maximum of 10 errors at the output of GCC, because sometimes you have more than 10.



4. -Wextra

you will have extra warnings.

So sometimes you have basic warnings, and then you have bonus warnings like more advanced small mistakes that you could have done on your C program.



### 1.3.5 执行其他文件夹里的可执行文件

```
[chenjj@node100 10-C_program]$ mkdir folder
[chenjj@node100 10-C_program]$ cp hello folder/.
[chenjj@node100 10-C_program]$ ./folder/hello 
Hello world!
```



### 1.3.6 通过绝对路径，执行可执行文件

以/开头，而不是.

```
[chenjj@node100 10-C_program]$ ./public/home/jlyang/chenjj/10-C_program/folder/hello
-bash: ./public/home/jlyang/chenjj/10-C_program/folder/hello: 没有那个文件或目录
[chenjj@node100 10-C_program]$ /public/home/jlyang/chenjj/10-C_program/folder/hello
Hello world!
```



# 2 Managing memory with Linux

## 2.1 Memory representation, RAM, cells, word, byte, bit, memory address

### 2.1.1 RAM(Random Access Memory) and Non-volatile memory

The term memory refers to the hardware in the computer that is involved in storing information for use in   the computer.

We distinguish between two different types of memory.

**RAM**, short for Random Access Memory, is temporary memory that is easy and quick to access and, for example, used to execute programs.
We also call this type of storage volatile memory.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200423001455888.png" alt="image-20200423001455888" style="zoom:33%;" />



On the other hand, there is nonvolatile, or lasting memory for more permanent storage of data, for example, used to store files on the hard drive.

In the technical specification of a computer's hardware, you can see the distinction between the amount of storage available via the RAM and the available hard drive space.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200423001605778.png" alt="image-20200423001605778" style="zoom:33%;" />



### 2.1.2 Bit, byte, and word

The vast majority of computer programs uses the computer's RAM during execution.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200423001745794.png" alt="image-20200423001745794" style="zoom:25%;" />

Values of variables, for example, are stored in -- meaningful written to and read from -- Random Access Memory.

For simplicity, we may represent the Random Access Memory as a sequence of binary memory cells, each populated with **a 0 or a 1**. We call each such cell **1 bit**.

By grouping several of these cells or bits together, we create what is called a **word**.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200423001952979.png" alt="image-20200423001952979" style="zoom:25%;" />

A word is the fundamental unit of data that can be moved between the RAM and the computer processor.

The size of a word is thus expressed in number of bits -- that is, number of memory cells -- or in bytes.

**1 byte= 8 bits**



### 2.1.3 一个word代表的bits

Modern personal computers and modern processors more ordinarily tend to use 8, 16, 32, or even 64 bits to form one word, though other word sizes are possible.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200423002204728.png" alt="image-20200423002204728" style="zoom:33%;" />

These particular word sizes emerge historically as a result of the hardware architecture, but they have evolved over time.



### 2.1.4 为什么内存要打包成word

Why would one want to group memory cells into words?

Well, this allows for the addressing of memory.

In fact, an address is assigned to each word. We also call this a **memory address**.

The computer address is a whole number that describes **the location of the word in the computer memory**.



**举例**

For example, imagine the computer whose word length is 8 bits.

Suppose, in addition, that this computer can store a total of four words. It's not a very big computer.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200423002520333.png" alt="image-20200423002520333" style="zoom:33%;" />

One could then address the computer's memory by assigning an address to each of the four words, just like you would assign an address to each of four houses on a street.

Each word gets a number as its address.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200423002626561.png" alt="image-20200423002626561" style="zoom:33%;" />



### 2.1.5 address是怎么安排的？

The address 0 would be used for the first word : that is, the first 8 memory cells.

The address 1 would be used for the second word : the next 8 memory cells.

The address 2 would be used for the third word, and the address 3 would be used for the fourth word.

In the C programming language, it is possible to get these memory addresses during the execution of a program.

If I use a variable in my program that stores an integer value, then not only could I find and use this value during my program, but equally well, I could obtain the memory location - that is, the address where the value is stored.



### 2.1.6 这种内存的优点

The use of memory addresses allows low-level access to the computer by allowing direct access to the computer's memory. One could literally move through the computer's memory from word to word.

This technique allows for optimization of memory usage at a very precise level, or of performance in terms of execution speed.

This is an extremely powerful tool for application developers.

So now you know that each variable has its own address, and that memory is composed of bits -- cells -- that are organized into words.



## 2.2 Manage the memory with the command line: free, top, htop

#### 2.2.1 free

#### 2.2.1.1 free -help

```
[chenjj@node100 10-C_program]$ free -help
free：无效选项 -- e

Usage:
 free [options]

Options:
 -b, --bytes         show output in bytes
 -k, --kilo          show output in kilobytes
 -m, --mega          show output in megabytes
 -g, --giga          show output in gigabytes
     --tera          show output in terabytes
 -h, --human         show human-readable output
     --si            use powers of 1000 not 1024
 -l, --lohi          show detailed low and high memory statistics
 -t, --total         show total for RAM + swap
 -s N, --seconds N   repeat printing every N seconds
 -c N, --count N     repeat printing N times, then exit
 -w, --wide          wide output

     --help     display this help and exit
 -V, --version  output version information and exit

For more details see free(1).
```



#### 2.2.1.2 free命令

```
free -m
free -k
free -b
```



### 2.2.2 top

see how many bytes are used is by using top.



#### 2.2.2.1 top -help

```
[chenjj@node100 ~]$ top -help
  procps-ng version 3.3.10
Usage:
  top -hv | -bcHiOSs -d secs -n max -u|U user -p pid(s) -o field -w [cols]
```



#### 2.2.2.2 top

```
top
```

回车：

```
top - 11:09:14 up 44 days, 19:29, 44 users,  load average: 1.14, 1.08, 0.98
Tasks: 565 total,   3 running, 550 sleeping,  12 stopped,   0 zombie
%Cpu(s):  3.4 us,  0.2 sy,  0.0 ni, 96.4 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem : 65851936 total, 19501092 free,  1468620 used, 44882224 buff/cache
KiB Swap: 67108860 total, 66090620 free,  1018240 used. 61562048 avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND                                                      
 2301 liujie    20   0 2959652 133812  28604 R 100.3  0.2  35:35.56 python                                                       
 2258 root      20   0  295144  11712    920 R   8.3  0.0   4700:31 pcnt                                                         
 3262 nobody    20   0  155956   2632    448 S   2.3  0.0   1351:28 psvr                                                         
18795 chenjj    20   0  157892   2728   1592 R   0.7  0.0   0:00.18 top                                                          
23733 root      20   0 2742856  45484   4004 S   0.7  0.1  93:21.06 pbs_server                                                   
 1631 root      20   0  106044    492    380 S   0.3  0.0   3:52.03 sshd                                                         
 2349 root      20   0  135936   1680    596 S   0.3  0.0 168:38.61 pcnt                                                         
 2360 root      20   0  132456    736    496 S   0.3  0.0  50:07.88 pcnt                                                         
 3276 nobody    20   0  155956    796    304 S   0.3  0.0 215:37.10 psvr                                                         
23756 root      20   0  223712   6692   2848 S   0.3  0.0  19:19.18 trqauthd                                                     
    1 root      20   0  193340   3236   1576 S   0.0  0.0   9:17.34 systemd                                                      
    2 root      20   0       0      0      0 S   0.0  0.0   0:02.16 kthreadd                                                     
    3 root      20   0       0      0      0 S   0.0  0.0   1:51.98 ksoftirqd/0                                                  
    8 root      rt   0       0      0      0 S   0.0  0.0   0:03.18 migration/0                                                  
    9 root      20   0       0      0      0 S   0.0  0.0   0:00.00 rcu_bh                                                       
   10 root      20   0       0      0      0 S   0.0  0.0  53:28.80 rcu_sched                                                    
   11 root      rt   0       0      0      0 S   0.0  0.0   0:08.47 watchdog/0                                                   
   12 root      rt   0       0      0      0 S   0.0  0.0   0:08.39 watchdog/1                                                   
   13 root      rt   0       0      0      0 S   0.0  0.0   0:02.85 migration/1                                                  
   14 root      20   0       0      0      0 S   0.0  0.0   1:21.51 ksoftirqd/1                                                  
   17 root      rt   0       0      0      0 S   0.0  0.0   0:06.72 watchdog/2                                                   
   18 root      rt   0       0      0      0 S   0.0  0.0   0:05.41 migration/2  
```


You can see that 3,256 kilobytes of memory is used, and here is the number that is free, and here we have a lot of programs running on the system, and we can sort them by memory.

But here you cannot see the column that says memory. Yes, we can see percent of CPU, but where is present memory doesn't exist.

Well, here it is VSZ that stands for Virtual Size, and the Virtual Size is indeed the **virtual memory for each program running on the system**.
We won't go into the details of why it is called virtual memory, but sometimes on some versions of the top that are installed on some Linux, you will have **VIRT** instead of the VSZ like this.



#### 2.2.2.3 M key

So let's try to push and M key. 

Type the M key, and here it just started all the programs, all the commands running, by VSZ.

From top to bottom, you can see that the first one is using 1,512 kilobytes of memory, and so forth.

So that is sorted by memory. 



#### 2.2.2.4 S key

And now if we hit the S key,
we go into a special visualization of the top command that is only showing the memory.
And indeed we have only one program running here, one user program that is named top, that is the actual program running.

And we can see that it is using 1,496 kilobytes of memory, and this is the same column as VSZ.



#### 2.2.2.5 Q key

All right, let's quit stop by hitting Q.



### 2.2.3 htop （我使用的linux系统上无法使用）

And the last thing I want to show you is how to see the memory consumption using htop.

So it's a visual representation of top, a little bit more advanced as you know.

Here you have little visualization of the memory.

We can see that we are using 2 out of 25 megabytes, so here are the used megabytes, and here the free ones.

And here we can see that it is sorted by CPU percent, but we can change that by pressing F6, which means sort by, as you can see in the menu at the bottom. 

So on my keyboard, I have to hit the function activate button key, which is fn.

And then F6, and here you have a menu on the left : Sort by, with the up and down arrows, you can select an option here, and we want to select M_SIZE, which stands for memory size.

I select that and I press the Enter key, and indeed, you can see that now it is ordered by the VIRT column.

Virtual memory, which is indeed the quantity of memory that is used by each command.

So the first line here is using 1,512 kilobytes and htop, as you can see here, is using 1,496 kilobytes of memory.



### 2.2.4 本节小结

That's it, so you know how to use free, top, and htop to see how much memory is used by your program.

And indeed, to control if a program is using too much memory on the system and putting too much pressure, maybe you can kill it if it is too big in memory.

So here is how to manage the memory on the Linux system.



## 2.3 Memory consumption of a program using htop, virtual memory

跳过本节，因为htop没用



## 2.4 Reboot Weblinux if needed

同样跳过。



# 3 Scanf and interactive programs in C

## 3.1 Interactive programs in C using scanf, fflush

### 3.1.1 printf is buffered

问出3个问题，每个问题自带\n；一一scanf输入答案。

如果3个问题，都漏了\n，那么不会提示问题；但是输入3个答案后，3个问题会一股脑在一行中出现。



因为printf is buffered。（buffered，缓冲的）

What is a buffer? It's a quantity of memory.

And the buffer ends when there is a newline backslash n in the printf.

Because here, we don't have any newline on any of the printf, it will only print all the printf at the end of the program.



程序：

```c
#include <stdio.h>

int main(void){
    char firstname[30];
    char familyname[30];
    int age;
    printf("What is your firstname?\n");
    scanf("%s", firstname);
    printf("What is your familyname?\n");
    scanf("%s", familyname);
    printf("What is your age?\n");
    scanf("%d", &age);
    printf("%s %s %d\n", firstname, familyname, age);
    return 0;
}
```





### 3.1.2 fflush(stdout)

But what we can do in the C programming language is to force to print the buffer even if there is no backslash n.
And to do that, we have to modify the source code. And we have to do just after each printf, a new instruction to flush the buffer.

It means to force the buffer to print on the screen. And to do that, it's fflush.
And we want to flush the standard upwards.
So it will be stdout.

Let's do that after each printf : **fflush(stdout)**

And the last one fflush(stdout). I don't need any flush for the last printf because the last instruction is just after.
And it will exit the program and force the flushing of all the buffers. So it will indeed print the last printf.
Let's try that ; we hit the run button.

这样，3个问题就会一一出现了。



### 3.1.3 取决于Linux系统的版本

So remember, if you are a C programmer and you ask for user input, be aware that you have to use a newline or you have to flush stdout with fflush like this, so that the user can see what's happening before you ask for an input from the user.

Also I would like to mention that some systems, some Linux systems, don't have the same behavior.
And they will print even if there is no backslash n, even if there is no newline at the end of a printf.

So it really depends on which version of the Linux system you have installed and on which version of the C programming library you are using.

But in webLinux and on many other Linux systems, you will have this behavior.

And you have to be very careful because your program, if you are using this kind of interaction, has to take
into account systems that don't flush automatically the printf without newlines.

**我在cluster 10上，printf没有\n，也会一句句出现**



## 3.2 Use scanf and file redirection to simulate an input

### 3.2.1 回顾echo

```
[chenjj@node100 10-C_program]$ echo "hello"
hello
[chenjj@node100 10-C_program]$ echo "hello" > f1.txt
[chenjj@node100 10-C_program]$ cat f1.txt 
hello
```



### 3.2.2 将内容传递为C语言程序name.c

#### 3.2.2.1 准备好文本

(以先Enter，再Control + D退出）：

```
[chenjj@node100 10-C_program]$ cat > answers
Jiajia
Chen
1
```



#### 3.2.2.2 方法1：cat

```
[chenjj@node100 10-C_program]$ cat answers | ./name
What is your firstname?
What is your familyname?
What is your age?
Jiajia Chen 1
```



#### 3.2.2.3 方法2：<

```
[chenjj@node100 10-C_program]$ ./name < answers 
What is your firstname?
What is your familyname?
What is your age?
Jiajia Chen 1
```



## 3.3 Don’t use scanf, use fgets getline or readline

### 3.3.1 scanf存在的问题

scanf可能会出问题，因为它不仅用new line区分，也用空格区分。

输入Remi Sharrock 18，就是说firstname是Remi，familyname是Sharrock，年龄是18。



### 3.3.2 使用fgets或getline或readline

Instead of scanf before a string, you should use both **f get s**.

But then you will have all the spaces and also the new line character at the end.

So you will get all the characters, even the newline characters.

So you will have to get rid of that character if you don't want it. Also, you can use getline.

And **getline** is a function that is compatible on POSIX systems, so not all of the systems.

And also, you can use on Linux the **gnureadline**, but it's only compatible on Linux operating systems.
So if you want to know more about those functions,
you can search on the internet.
And if you want to know more how to program in C,
I invite you to take other courses on how to program in C.