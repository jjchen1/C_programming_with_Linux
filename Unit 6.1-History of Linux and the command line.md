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

### 1.2.1 



PETRA : In this video, we're going to tell you
about the genesis of Unix, the most advanced operating system of its time
that introduced many concepts still used in all modern operating systems.

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409010029802.png" alt="image-20200409010029802" style="zoom:33%;" />



REMI : The era of modern computers emerged
with the appearance of integrated circuits and magnetic disks.
Rather than using individual transistors connected by wires
to control the flow of electrons, integrated circuits
combine, or integrate, electronic circuits into a single device.
PETRA : This was also the time when we
started to see families of compatible computers, such as the IBM System/360,
a system announced by IBM in 1964 in which
a clear distinction between architecture and implementation was made,
allowing for the release of various compatible designs at different prices.
REMI : In addition, this marks the time
when the first ideas relating to Unix were born.
It all started with the MAC project, project on mathematics and computation,
founded by the Massachusetts Institute of Technology
and funded by the US military research funding agency ARPA and the US National
Science Foundation.
PETRA: The main goal of this large scale project
was to realize a timesharing system that would allow a wide community of users
to simultaneously access the hardware and software
resources of a single computer from multiple locations.
Six years after its inception, project MAC,
jointly with Bell Laboratories and General Electric,
developed MULTICS, the Multiplexed Information and Computing Service.
REMI : This service was no longer just about computer resource
timesharing, but evolved to also incorporate
features such as file sharing, file management, and system security.
Multiplexing is a technique of sending multiple pieces of information
over a communication link at the same time
in the form of a single complex signal.
Multiplexing makes it possible to share the same resource
between several users.
PETRA : General Electric's contribution to the MULTICS project
was to design and build the underlying machine,
whereas Bell Labs took on the design and writing of the operating system code,
in particular the aspects related to remote access by multiple users.
The realization of this ambitious project
proved much more difficult than expected.
REMI : The system only began to operate in 1969 on the GE-645
computer designed by General Electric.
But its performance was far from the originally set targets.
Bell Labs pulled out of the project that same year.
PETRA : Following the withdrawal of Bell Labs from the MULTICS project,
some Bell Labs engineers working on the project,
led by Ken Thompson and Dennis Ritchie, decided
to pursue an alternative approach to the system, which they considered
to be cumbersome and complex.
Using their experience, they set out to realize a minimal system
on a small machine.
Well, small.
Everything is relative.
Look at the picture.
In 1969, having access to a little-used DAC PD7,
they began the development of a single-user operating system
on their own account and without any support from Bell Labs.
As a pun on MULTICS, they called the system UNICS.
REMI : In 1970, the system changed from single user to multiple users.
And the spelling of its name morphed to Unix.
At the time, the system was written in the B programming
language invented by Ken Thompson.
PETRA : In 1971, Dennis Ritchie improved his colleague Ken's language
and called it the new B. By 1972, the changes to the B language
became so significant that Dennis Ritchie renamed his new language
the C language.
Ken jumped on the opportunity and rewrote
all of the code making up the Unix operating system in this improved C
programming language.
REMI : After two to three years of work,
Ken sent the C source code of the Unix operating system
to universities and research centers for educational purposes
all around the world.
I remember a professor at my university saying
that he received a magnetic tape of the C source code of the Unix operating
system in 1976.
He had difficulties with the customs at the French border,
since nobody knew what these big magnetic tapes were.
PETRA : From 1975 on, a very active community
emerged around Unix and the C programming language,
with the other notable developers of Unix being Douglas McElroy--
who is now right here at Dartmouth--
Joseph Ossanna, and Rudd Canaday.
Various different versions of Unix saw the light of the day,
in particular the various machines constructed by different computer
builders.
REMI : In 1978, Dennis Ritchie--
jointly with his pedagogically-inclined colleague,
Brian Kernighan-- wrote the book The C Programming Language.
This was the boom of popularity of Unix and the C programming language.
And a few years later, in 1983 when I was born,
Ken and Dennis received the highest distinction
in the computer science field for this invention, the Turing Prize.
PETRA : The basics of Unix are ubiquitous today.
Did you know that the Mac operating system installed on Apple computers
is a derivative of Unix, as is the iOS operating system for iPhone, iPad,
the Android system for Google phones, and even the Linux
system installed on the vast majority of today's service and connected objects?

