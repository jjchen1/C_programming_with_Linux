[TOC]

# 1 Discovering operating systems

## 1.1 Operating systems genesis: definition, services (files, memory, processes), key dates

### 1.1.1  A number of different operating systems.

Windows by Microsoft, 

macOS or iOS by Apple, 

Android by Google.

Linux or even Unix.



### 1.1.2 Unix, Linux.

Unix has been around quite a bit longer than Linux.
But these two operating systems are indeed related.
Linux is a Unix-like operating system that is open source.
This means that the Linux kernel, created by Linus Torvalds and enhanced and expanded upon by thousands of programmers, is available to the world for free.



### 1.1.3 What is an operating system?

An operating system is an intermediary between the hardware (memory, hard disk, processor, Wi-Fi network cards, et cetera) and the applications that we all use.

Indeed, you as the user use the services rendered by applications.

Applications use the services provided by the operating system.

And the operating system exploits the hardware resources that are at its disposal to render these services to the applications.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409002949351.png" alt="image-20200409002949351" style="zoom:33%;" />



### 1.1.4 Some examples of services provided by the operating system

1. File management.

That is, managing the logical tree structure of files and their physical layout on the storage device, also known as the hard drive.



2. Memory management.

Memory can be shared between several running processes.



3. Management of running applications.

We are talking about running processes. You can run an application, kill a running application, et cetera.



4. Management of inputs and outputs.

For example, network cards to access the internet, sound cards, video cards, printers, et cetera.



### 1.1.4 the history of the operating system

#### 1.1.4.1 第一台计算机的发明

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409004151732.png" alt="image-20200409004151732" style="zoom:33%;" />

In the mid-1940s, the first computers were built using vacuum tubes. Vacuum tubes are evacuated glass containers that can control electric current and can therefore function as on-off switches. 



<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409004127007.png" alt="image-20200409004127007" style="zoom:33%;" />

These tubes are rather large. And each of these first computers used quite a few of them, resulting in huge machines that filled entire rooms while performing more slowly than a modern hand-held calculator.

Programming of these machines had to be done manually by moving around tubes. And input-output was very limited.

In fact, the programmer was also in charge of operating the machine via direct interaction, which meant a lot of heavy lifting.



So in fact, the designer of the computer was also the builder of the computer, and at the same time the programmer as well as the operator.



#### 1.1.4.2 晶体管的发明和穿孔卡片



<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409003938069.png" alt="image-20200409003938069" style="zoom:50%;" />

Everything changed with the invention of the transistor.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409005411604.png" alt="image-20200409005411604" style="zoom:50%;" />

At the same time, this marks the beginning of operating systems via the appearance of punch cards.



Punch cards are cards with holes, punches, placed in specific locations so as to encode computer programs and data that can be loaded via the computer's punch card reader into the computer's memory.



Punch cards can also be used as computer output.

A separation of roles emerged. A programmer produced punch cards-- programs that input data-- and an operator physically loaded these cards into the computer and on-loaded the computer's output.



That is when the operating system was invented to manage the memory, the processes, programs loaded
while running, and these punch cards, inputs and outputs, reading punch cards, writing the results.



We can therefore say that it was in the mid-1960s that operating systems were invented.



## 1.2 UNIX genesis: MAC projet @ MIT, MULTICS, Thompson & Ritchie

### 1.2.1 1964年，集成电路和磁盘

We're going to tell you about the genesis of Unix, the most advanced operating system of its time that introduced many concepts still used in all modern operating systems.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409010029802.png" alt="image-20200409010029802" style="zoom:33%;" />



The era of modern computers emerged with the appearance of integrated circuits and magnetic disks.

Rather than using individual transistors connected by wires to control the flow of electrons, integrated circuits combine, or integrate, electronic circuits into a single device.



### 1.2.2 1964年，IBM System/360

This was also the time when we started to see families of compatible computers, such as the IBM System/360, a system announced by IBM in 1964 in which a clear distinction between architecture and implementation was made, allowing for the release of various compatible designs at different prices.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409131425722.png" alt="image-20200409131425722" style="zoom:33%;" />



### 1.2.3 1963-1964年， MAC project

In addition, this marks the time when the first ideas relating to Unix were born.

It all started with the **MAC project**, project on mathematics and computation, founded by the Massachusetts Institute of Technology and funded by the US military research funding agency ARPA and the US National Science Foundation.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409131651022.png" alt="image-20200409131651022" style="zoom:33%;" />

The main goal of this large scale project was to realize a timesharing system that would allow a wide community of users to simultaneously access the hardware and software resources of a single computer from multiple locations.



### 1.2.4 MULTICS

Six years after its inception, **project MAC**, jointly with Bell Laboratories and General Electric, developed **MULTICS**, the Multiplexed Information and Computing Service.

This service was no longer just about computer resource timesharing, but evolved to also incorporate
features such as file sharing, file management, and system security.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409132500911.png" alt="image-20200409132500911" style="zoom:33%;" />



### 1.2.5 Multiplexing （多路传输）

Multiplexing is a technique of sending multiple pieces of information over a communication link at the same time in the form of a single complex signal.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409132727801.png" alt="image-20200409132727801" style="zoom:33%;" />

Multiplexing makes it possible to share the same resource between several users.

### 1.2.6 “2 business”

General Electric's contribution to the MULTICS project was to design and build the underlying machine, whereas Bell Labs took on the design and writing of the operating system code, in particular the aspects related to remote access by multiple users.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409133006945.png" alt="image-20200409133006945" style="zoom:33%;" />

The realization of this ambitious project proved much more difficult than expected.



### 1.2.7 1969年，GE-645 System

The system only began to operate in 1969 on the GE-645 computer designed by General Electric.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409133134747.png" alt="image-20200409133134747" style="zoom:33%;" />

But its performance was far from the originally set targets. Bell Labs pulled out of the project that same year.



### 1.2.8 制造Unix的初衷：想要a small machine

Following the withdrawal of Bell Labs from the MULTICS project, some Bell Labs engineers working on the project, led by Ken Thompson and Dennis Ritchie, decided to pursue an alternative approach to the system, which they considered to be cumbersome and complex.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409133342629.png" alt="image-20200409133342629" style="zoom:33%;" />

Using their experience, they set out to realize a minimal system on a small machine.



### 1.2.9 DAC PD7；1969年，UNICS

Everything is relative. Look at the picture.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409133529386.png" alt="image-20200409133529386" style="zoom:33%;" />

In 1969, having access to a little-used DAC PD7, they began the development of a single-user operating system on their own account and without any support from Bell Labs.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409133706685.png" alt="image-20200409133706685" style="zoom:33%;" />

As a pun on MULTICS, they called the system UNICS.



### 1.2.10 1970年，UNIX

In 1970, the system changed from single user to multiple users. And the spelling of its name morphed to Unix.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409134014722.png" alt="image-20200409134014722" style="zoom:33%;" />

At the time, the system was written in the B programming language invented by Ken Thompson.

In 1971, Dennis Ritchie improved his colleague Ken's language and called it the new B. 



### 1.2.11 1972年，C language

By 1972, the changes to the B language became so significant that Dennis Ritchie renamed his new language the C language.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409134240262.png" alt="image-20200409134240262" style="zoom:33%;" />

Ken jumped on the opportunity and rewrote all of the code making up the Unix operating system in this improved C programming language.

After two to three years of work, Ken sent the C source code of the Unix operating system to universities and research centers for educational purposes all around the world.

I remember a professor at my university saying that he received a magnetic tape of the C source code of the Unix operating system in 1976.

He had difficulties with the customs at the French border, since nobody knew what these big magnetic tapes were. 



### 1.2.12 1975年， a very active community emerged

From 1975 on, a very active community emerged around Unix and the C programming language,
with the other notable developers of Unix being Douglas McElroy-- who is now right here at Dartmouth--
Joseph Ossanna, and Rudd Canaday.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409134434187.png" alt="image-20200409134434187" style="zoom:33%;" />

Various different versions of Unix saw the light of the day, in particular the various machines constructed by different computer builders.



### 1.2.13 1978年，《The C Programming Language》

In 1978, Dennis Ritchie-- jointly with his pedagogically-inclined colleague, Brian Kernighan-- wrote the book The C Programming Language.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409140646437.png" alt="image-20200409140646437" style="zoom:33%;" />

This was the boom of popularity of Unix and the C programming language.



### 1.2.14 1983年，the Turing Prize

And a few years later, in 1983 when I was born, Ken and Dennis received the highest distinction in the computer science field for this invention, the Turing Prize.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409140752244.png" alt="image-20200409140752244" style="zoom:33%;" />



### 1.2.15 Unix无处不在

The basics of Unix are ubiquitous today.

Did you know that the Mac operating system installed on Apple computers is a derivative of Unix, as is the iOS operating system for iPhone, iPad, the Android system for Google phones, and even the Linux system installed on the vast majority of today's service and connected objects?



## 1.3 Activity: OS, UNIX, history and genesis

![image-20200409145008958](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409145008958.png)



之前错选：new B，又错选GE-645，第3次才选对。



## 1.5 Linux genesis and history: GNU, Stallman, GPL, Linus Torvals, Linux

### 1.5.1 1980年，Unix被大学和研究中心广泛使用，但Unix要付费

By the early 1980s, the Unix operating system had been largely adopted by universities and research
centers which led to further adoption by many startups and companies.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409141734603.png" alt="image-20200409141734603" style="zoom:33%;" />



### 1.5.2 1983年，the Turing Award，GNU project

In 1983, Unix inventors Dennis Ritchie and Ken Thompson received the Turing Award for their invention.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409141822135.png" alt="image-20200409141822135" style="zoom:33%;" />

And that same year, Richard Stallman of MIT launched the GNU Project.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409141909170.png" alt="image-20200409141909170" style="zoom:33%;" />

GNU is a recursive acronym, referring to itself, that stands for GNU is Not Unix.
The GNU Project is an open and free, collaborative project to develop and provide software compatible with Unix.

The big difference between the GNU Project and Unix is that Unix is owned by Bell Labs, which sells licenses for use or modification, while the GNU Project is free, and anyone can use or modify the entire project.



### 1.5.3 1989年，Free as in Freedom

Richard Stallman is a strong advocate for free and open source software.

In 1989, he conceived of the GNU General Public License, which aims to preserve the freedom to use, study, modify, and distribute software and its derivative versions.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409142039369.png" alt="image-20200409142039369" style="zoom:33%;" />



### 1.5.4 1990年，GPU项目，已经具备多种软件

REMI : By 1990, the GNU Project included a lot of software already, text editors, a graphical user interface similar to Windows, libraries, the GNU C Compiler-- GCC-- a C language compiler, et cetera.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409142159154.png" alt="image-20200409142159154" style="zoom:33%;" />

### 1.5.5 1991年，免费的Linux应运而生

The problem was that one had to use this free software on the Unix operating system that itself is proprietary and not open or free.

This is where Linus Torvalds, a 21-year-old Finnish computer science student at the University of Helsinki, intervened. **He was frustrated by these proprietary licenses that limited the use of the operating system.**

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409142419752.png" alt="image-20200409142419752" style="zoom:33%;" />



On August 25, 1991, he sent a message to the community that started like this, "Hi, everyone. I am doing a free operating system. It's just a hobby. It will not be as big and as professional as the GNU Project."

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409142453158.png" alt="image-20200409142453158" style="zoom:33%;" />

This project, which later became the Linux kernel, was written specifically to be independent of an operating system, and was meant to run on Linus Torvalds' PC, with an 83.86 processor.

Development was done using the GNU C Compiler, which to this day is still the main choice for compiling Linux.

Just as in the case of the GNU Project, the community formed. And developers of the GNU Project quickly integrated free software to run on the Linux kernel, which itself is also free.



### 1.5.6 1992年，第1个Linux distributions

In 1992, the first Linux distributions were released and consisted of the free Linux operating system and a collection of free GNU Project software tools, such as editors, libraries, compilers, et cetera.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409142720292.png" alt="image-20200409142720292" style="zoom:33%;" />

By 1993, there were already more than 100 developers from around the world who worked on modifying and improving Linux.



### 1.5.7 受欢迎的Linux版本出世，如：Debian

1993 was also the year of some very popular Linux distributions, for example Debian.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409143011703.png" alt="image-20200409143011703" style="zoom:33%;" />



### 1.5.8 90年代末，硬件公司支持Linux

By the end of the '90s, the major computer manufacturers Dell, IBM, and HP announced compatibility of their hardware with Linux.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409143125686.png" alt="image-20200409143125686" style="zoom:33%;" />



### 1.5.9 2000年代，Linux用于web服务

During the 2000s, Linux was deployed more and more as the operating system that runs web servers.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409143214630.png" alt="image-20200409143214630" style="zoom:33%;" />



### 1.5.10 Linux和Unix-based操作系统，市场份额很大

In the 2010s, Linux and Unix-based operating systems became the most widely used systems on internet servers, taking about 70% of the market share, and smartphones, around 90%, since the Android operating
system is based on Linux and iOS is based on Unix.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409143332719.png" alt="image-20200409143332719" style="zoom:33%;" />

These operating systems also started dominating supercomputers, for example for scientific calculations or for the film and special effects industry, around 99% of the market share.

Linux and Unix-based operating systems can further be found in game consoles, for example Playstation, internet boxes, Wi-Fi routers, and connected objects such as internet-connected watches.

The Linux operating system or other Unix derivatives have become a part of many aspects of our everyday life.



# 2 Manipulating the command line interface

## 2.1 Command line interface, prompt, command options and files data, command cal as example

### 2.1.1 command line interface (CLI)

A command line interface, sometimes abbreviated CLI, is a human machine interface in which communication between the user and the computer takes place in text mode.

The user types a command--that is, they type of the text using the keyboard to ask the computer to perform an operation.

The computer then displays text corresponding to the result of the execution of the command or text
corresponding to the questions that an invoked software application asks of the user.



### 2.1.2 A command line interface

A command line interface can also be used to launch the execution of various software applications
that use a command interpreter as well as for dialogue with a user.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409151426229.png" alt="image-20200409151426229" style="zoom:33%;" />

It is at the core of the interaction between a user and the computer or any other computing equipment.

When a command line interface is ready to receive a command from the user.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409151524438.png" alt="image-20200409151524438" style="zoom:33%;" />

It indicates this by displaying a command prompt.

This prompt typically consists of some information at the beginning of the line, usually the user's account name, or the computer name, or the current working directory or the date.

And it ends with a well-known character, often the dollar, or the pound sign or the greater than sign.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409151610130.png" alt="image-20200409151610130" style="zoom:33%;" />

This prompt lets the user know that the system is ready to receive a command.



### 2.1.3 command的格式

One of the features of the Unix operating system and, by inheritance, the Linux operating system
is that from its earliest beginnings on, it has had at its disposal more than 100 software applications, often performing very simple tasks and, most importantly, all usable from the command line.

The elementary commands are of the form-- well, command at the beginning, then space, options, than space, then files_or_data-- knowing that the options and the files or data are optional.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409151950204.png" alt="image-20200409151950204" style="zoom:50%;" />



The command appearing at the beginning of the line is almost always the name of a software application. This can be an operating system command or another software application written by a user, often in the C programming language.

A command line option modifies the execution of a command. The effect of the option depends on the command.

Generally, the options immediately follow the name of the command on the command line and they are separated by spaces.



### 2.1.4 the files or data

Finally, the files or data are the program entries. 

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409152208829.png" alt="image-20200409152208829" style="zoom:50%;" />

For example, if you want to run the application that displays a calendar in text mode, you type the command cal and press the Enter key. And here's the result. 

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409152316751.png" alt="image-20200409152316751" style="zoom:33%;" />



If we add the minus j option to it, it displays the calendar in Julian days.

That's the number of days elapsed since January 1st, so we type the command cal minus j, press the Enter key and here's the calendar in Julian days.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409152354930.png" alt="image-20200409152354930" style="zoom:33%;" />



## 2.2 First commands: echo 'hello world', date, cal, history, whoami, hostname, uptime, clear, command not found, man, command options

### 2.2.1 命令：whoami

回车后，出现用户名。

如，登录cluster 10，就得到：chenjj

即，username。



### 2.2.2 如果不知道whoami怎么用，命令：whoami --help

回车后，出现:

```
用法：whoami [选项]...
显示与当前的有效用户ID 相关联的用户名。
与id -un 相同。

      --help		显示此帮助信息并退出
      --version		显示版本信息并退出

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
请向<http://translationproject.org/team/zh_CN.html> 报告whoami 的翻译错误
要获取完整文档，请运行：info coreutils 'whoami invocation'
```



### 2.2.3 命令：id

回车，得到：

```
uid=1100(chenjj) gid=1002(jlyang) 组=1002(jlyang),1007(fat)
```

the user id, uid=1100

the group id, gid=1002



### 2.2.4 命令：logname

先用“logname --help”查看使用方法：

```
用法：logname [选项]
显示当前用户的名称。

      --help		显示此帮助信息并退出
      --version		显示版本信息并退出

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
请向<http://translationproject.org/team/zh_CN.html> 报告logname 的翻译错误
要获取完整文档，请运行：info coreutils 'logname invocation'
```



输入：logname

得到：chenjj

和username一样



### 2.2.5 命令：echo

1. 输入：echo hello

输出：```hello```



2. 输入：echo $0

不输出$0，而是输出interpreter中变量$0代表的值：```-bash```

这代表shell，shell是用于解释Linux中的命令的。shell是一个应用，一个软件。

（视频中，输出```sh```）



### 2.2.6 命令：hostname

1. 输入：hostname --help

输出：

```
Usage: hostname [-b] {hostname|-F file}         set host name (from file)
       hostname [-a|-A|-d|-f|-i|-I|-s|-y]       display formatted name
       hostname                                 display host name

       {yp,nis,}domainname {nisdomain|-F file}  set NIS domain name (from file)
       {yp,nis,}domainname                      display NIS domain name

       dnsdomainname                            display dns domain name

       hostname -V|--version|-h|--help          print info and exit

Program name:
       {yp,nis,}domainname=hostname -y
       dnsdomainname=hostname -d

Program options:
    -a, --alias            alias names
    -A, --all-fqdns        all long host names (FQDNs)
    -b, --boot             set default hostname if none available
    -d, --domain           DNS domain name
    -f, --fqdn, --long     long host name (FQDN)
    -F, --file             read host name or NIS domain name from given file
    -i, --ip-address       addresses for the host name
    -I, --all-ip-addresses all addresses for the host
    -s, --short            short host name
    -y, --yp, --nis        NIS/YP domain name

Description:
   This command can get or set the host name or the NIS domain name. You can
   also get the DNS domain or the FQDN (fully qualified domain name).
   Unless you are using bind or NIS for host lookups you can change the
   FQDN (Fully Qualified Domain Name) and the DNS domain name (which is
   part of the FQDN) in the /etc/hosts file.
```



输入：hostname

输出：```node100```

显示在这个系统中，计算机的name。

（视频中，运行WebLinux的计算机，其名字为openrisk）



### 2.2.7 命令：uname

1. 输入：uname --help

输出：

```
用法：uname [选项]...
输出一组系统信息。如果不跟随选项，则视为只附加-s 选项。

  -a, --all			以如下次序输出所有信息。其中若-p 和
				-i 的探测结果不可知则被省略：
  -s, --kernel-name		输出内核名称
  -n, --nodename		输出网络节点上的主机名
  -r, --kernel-release		输出内核发行号
  -v, --kernel-version		输出内核版本
  -m, --machine		输出主机的硬件架构名称
  -p, --processor		输出处理器类型或"unknown"
  -i, --hardware-platform	输出硬件平台或"unknown"
  -o, --operating-system	输出操作系统名称
      --help		显示此帮助信息并退出
      --version		显示版本信息并退出

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
请向<http://translationproject.org/team/zh_CN.html> 报告uname 的翻译错误
要获取完整文档，请运行：info coreutils 'uname invocation'
```



2. 输入：uname

输出：```Linux```

即，输出系统名



3. 输入：uname -a

输出：```Linux node100 3.10.0-693.5.2.el7.x86_64 #1 SMP Fri Oct 20 20:32:50 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux```

即，输出系统的所有信息



### 2.2.8 命令：history

输入：hhistory

输出了10014个以前的命令。



视频中的WebLinux，进入系统后，会自动生成2个命令；其余的命令，就都是视频中手动输入的。



在命令行中，按“↑”键，会出现上一个命令；再按一下“↑”键，会出现上上一个命令。

“↓”键的作用相反。



### 2.2.9 命令：uptime

1. 输入：uptime

输出：``` 19:27:22 up 31 days, 3:47, 38 users, load average: 0.07, 0.10, 0.14```

uptime will display how many minutes until the system was booted,

so here we can see the hour.

And then we can see that it is up for nine minutes now.

And you can just see a bunch of other statistics like the load average, which is the load average of the CPU.



### 2.2.10 命令：cal

1. 输入：cal

显示日历calendar：

```
      四月 2020     
日 一 二 三 四 五 六
          1  2  3  4
 5  6  7  8  9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30
```



数字9是变色的，所以现在是2020.4.9



2. 输入：cal --help

输出：

```
用法：
 cal [选项] [[[日] 月] 年]

选项：
 -1, --one        只显示当前月份(默认)
 -3, --three      显示上个月、当月和下个月
 -s, --sunday     周日作为一周第一天
 -m, --monday     周一用为一周第一天
 -j, --julian     输出儒略日
 -y, --year       输出整年
 -V, --version    显示版本信息并退出
 -h, --help       显示此帮助并退出
```



3. 输入：cal -j

输出：

```
         四月 2020         
 日  一  二  三  四  五  六
             92  93  94  95
 96  97  98  99 100 101 102
103 104 105 106 107 108 109
110 111 112 113 114 115 116
117 118 119 120 121
```

数字100是变色的，所以现在是距离2020年1月1日过了100天。



### 2.2.11 命令：date

输入：date

输出：```2020年 04月 09日 星期四 19:36:29 CST```



2. 输入：date --help

输出：

```
用法：date [选项]... [+格式]
　或：date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]
Display the current time in the given FORMAT, or set the system date.

Mandatory arguments to long options are mandatory for short options too.
  -d, --date=STRING         display time described by STRING, not 'now'
  -f, --file=DATEFILE       like --date once for each line of DATEFILE
  -I[TIMESPEC], --iso-8601[=TIMESPEC]  output date/time in ISO 8601 format.
                            TIMESPEC='date' for date only (the default),
                            'hours', 'minutes', 'seconds', or 'ns' for date
                            and time to the indicated precision.
  -r, --reference=文件		显示文件指定文件的最后修改时间
  -R, --rfc-2822		以RFC 2822格式输出日期和时间
				例如：2006年8月7日，星期一 12:34:56 -0600
      --rfc-3339=TIMESPEC   output date and time in RFC 3339 format.
                            TIMESPEC='date', 'seconds', or 'ns' for
                            date and time to the indicated precision.
                            Date and time components are separated by
                            a single space: 2006-08-07 12:34:56-06:00
  -s, --set=STRING          set time described by STRING
  -u, --utc, --universal    print or set Coordinated Universal Time (UTC)
      --help		显示此帮助信息并退出
      --version		显示版本信息并退出

给定的格式FORMAT 控制着输出，解释序列如下：

  %%	一个文字的 %
  %a	当前locale 的星期名缩写(例如： 日，代表星期日)
  %A	当前locale 的星期名全称 (如：星期日)
  %b	当前locale 的月名缩写 (如：一，代表一月)
  %B	当前locale 的月名全称 (如：一月)
  %c	当前locale 的日期和时间 (如：2005年3月3日 星期四 23:05:25)
  %C	世纪；比如 %Y，通常为省略当前年份的后两位数字(例如：20)
  %d	按月计的日期(例如：01)
  %D	按月计的日期；等于%m/%d/%y
  %e	按月计的日期，添加空格，等于%_d
  %F	完整日期格式，等价于 %Y-%m-%d
  %g	ISO-8601 格式年份的最后两位 (参见%G)
  %G	ISO-8601 格式年份 (参见%V)，一般只和 %V 结合使用
  %h	等于%b
  %H	小时(00-23)
  %I	小时(00-12)
  %j	按年计的日期(001-366)
  %k   hour, space padded ( 0..23); same as %_H
  %l   hour, space padded ( 1..12); same as %_I
  %m   month (01..12)
  %M   minute (00..59)
  %n	换行
  %N	纳秒(000000000-999999999)
  %p	当前locale 下的"上午"或者"下午"，未知时输出为空
  %P	与%p 类似，但是输出小写字母
  %r	当前locale 下的 12 小时时钟时间 (如：11:11:04 下午)
  %R	24 小时时间的时和分，等价于 %H:%M
  %s	自UTC 时间 1970-01-01 00:00:00 以来所经过的秒数
  %S	秒(00-60)
  %t	输出制表符 Tab
  %T	时间，等于%H:%M:%S
  %u	星期，1 代表星期一
  %U	一年中的第几周，以周日为每星期第一天(00-53)
  %V	ISO-8601 格式规范下的一年中第几周，以周一为每星期第一天(01-53)
  %w	一星期中的第几日(0-6)，0 代表周一
  %W	一年中的第几周，以周一为每星期第一天(00-53)
  %x	当前locale 下的日期描述 (如：12/31/99)
  %X	当前locale 下的时间描述 (如：23:13:48)
  %y	年份最后两位数位 (00-99)
  %Y	年份
  %z +hhmm		数字时区(例如，-0400)
  %:z +hh:mm		数字时区(例如，-04:00)
  %::z +hh:mm:ss	数字时区(例如，-04:00:00)
  %:::z			数字时区带有必要的精度 (例如，-04，+05:30)
  %Z			按字母表排序的时区缩写 (例如，EDT)

默认情况下，日期的数字区域以0 填充。
The following optional flags may follow '%':

  -  (hyphen) do not pad the field
  _  (underscore) pad with spaces
  0  (zero) pad with zeros
  ^  use upper case if possible
  #  use opposite case if possible

在任何标记之后还允许一个可选的域宽度指定，它是一个十进制数字。
作为一个可选的修饰声明，它可以是E，在可能的情况下使用本地环境关联的
表示方式；或者是O，在可能的情况下使用本地环境关联的数字符号。

Examples:
Convert seconds since the epoch (1970-01-01 UTC) to a date
  $ date --date='@2147483647'

Show the time on the west coast of the US (use tzselect(1) to find TZ)
  $ TZ='America/Los_Angeles' date

Show the local time for 9AM next Friday on the west coast of the US
  $ date --date='TZ="America/Los_Angeles" 09:00 next Fri'

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
请向<http://translationproject.org/team/zh_CN.html> 报告date 的翻译错误
要获取完整文档，请运行：info coreutils 'date invocation'
```

可知date命令的使用、选项、格式



3. 输入：date +"%T" 

输出：```19:39:14```

因为： %T	时间，等于%H:%M:%S



4. 输入：date +"%A %d %B %Y"

输出：```星期四 09 四月 2020```



### 2.2.12 命令：man

意味着： 命令的使用手册（manual）。

如：man cal

得到cal命令的使用手册。



man man也可以，这样能得到man命令的使用手册。

（但在视频的WebLinux中，man无法使用，因为manual文件很大，直接就没配置。）



在manual中，按键“q”，退出manual。



### 2.2.13 命令：clear

输入：clear

清除显示的所有命令记录；输入命令的行，出现在顶端。



## 2.5 Interactive commands: top, htop, nano, vim, how to get back to the prompt

### 2.5.1 命令行

终端命令行：

先是~，再是空格，$，然后是光标

~ $



等待输入命令，再按回车键，从而执行命令。

有时候，就会进入program，与user进行互动；直到你退出program，回到prompt（提示符）。



### 2.5.1 命令：top

1. 输入：top

进入top内了。



2. 输入：--help

输出：

```
Help for Interactive Commands - procps-ng version 3.3.10
Window 1:Def: Cumulative mode Off.  System: Delay 3.0 secs; Secure mode Off.

  Z,B,E,e   Global: 'Z' colors; 'B' bold; 'E'/'e' summary/task memory scale
  l,t,m     Toggle Summary: 'l' load avg; 't' task/cpu stats; 'm' memory info
  0,1,2,3,I Toggle: '0' zeros; '1/2/3' cpus or numa node views; 'I' Irix mode
  f,F,X     Fields: 'f'/'F' add/remove/order/sort; 'X' increase fixed-width

  L,&,<,> . Locate: 'L'/'&' find/again; Move sort column: '<'/'>' left/right
  R,H,V,J . Toggle: 'R' Sort; 'H' Threads; 'V' Forest view; 'J' Num justify
  c,i,S,j . Toggle: 'c' Cmd name/line; 'i' Idle; 'S' Time; 'j' Str justify
  x,y     . Toggle highlights: 'x' sort field; 'y' running tasks
  z,b     . Toggle: 'z' color/mono; 'b' bold/reverse (only if 'x' or 'y')
  u,U,o,O . Filter by: 'u'/'U' effective/any user; 'o'/'O' other criteria
  n,#,^O  . Set: 'n'/'#' max tasks displayed; Show: Ctrl+'O' other filter(s)
  C,...   . Toggle scroll coordinates msg for: up,down,left,right,home,end

  k,r       Manipulate tasks: 'k' kill; 'r' renice
  d or s    Set update interval
  W,Y       Write configuration file 'W'; Inspect other output 'Y'
  q         Quit
          ( commands shown with '.' require a visible task display window ) 
Press 'h' or '?' for help with Windows,
Type 'q' or <Esc> to continue 
```

这些都是关键词。

最重要的是：q，意味着quit，退出程序。

还有：Control + q



3. top中，包含memory usage , CPU usage, and the load average.

我们在运行一系列program。



### 2.5.2 命令：htop

这是一种top命令，但有一些额外功能。htop命令，需要install，才能使用。

see here the CPU consumption in a more graphical way, and also the memory consumption.



除了q和control + c，F10也可以退出program。

（此处我没自己尝试htop，因为系统没有自带。）



## 2.5.3 命令：nano

nano，是一款文件编辑器，非常基础的类型。

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409222043049.png" alt="image-20200409222043049" style="zoom:25%;" />

所以，可以通过G，得到帮助；通过X，退出程序……

所以，可以用Control + X，退出程序；

而Control + C后，没有退出程序，但下面的菜单发生变化：

![image-20200409222443491](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409222443491.png)



（后面还有一些内容，我跳过了。）



### 2.5.3 vim编辑器

1. 输入```vim```，回车，进入vim编辑器；



2. 输入```:q```，退出vim编辑器。



3. 在vim编辑器中，输入```i```，进入insert模式，输入i；

这时，无法退出vim编辑器，字母q或control+c，都无济于事。

需要按esc键，再输入```:q!```，可以强制退出，不保存之前的修改。



### 2.5.4 control + c

对绝大多数program而言，control + c可以退出程序。

如果不可行，用help查看退出的方法吧。



## 2.6 Play with commands: hello, worm, firework, rain, hanoi

下述命令，在视频的WebLinux上可行。

是一些有趣的游戏类命令。



1. 输入：hello

输出：Hello world！



2. 输入：worm

屏幕上出现绿色的线条在动，就像worm（虫子）一样。

（用control + c退出程序）



3. 输入：firework

屏幕上出现烟花动画。

（用control + c退出程序）



4. 输入：rain

屏幕上出现雨。

（用control + c退出程序）



5. 输入：honoi

屏幕上出现Honoi tower游戏：

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409225253285.png" alt="image-20200409225253285" style="zoom:50%;" />

（用Q退出程序。）



6. 输入：knight

出现文字版卡牌游戏：

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409225541415.png" alt="image-20200409225541415" style="zoom:50%;" />

（用X或Q退出程序。）