[TOC]

# 1 Modularizing a program

## 1.1 GCC details

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra program.c -lm -o program
```



### 1.1.1 -std=c11

the -std=C11 tells the compiler which C standard to use.

The C standard we're using here is C11. That's a modern C standard.



### 1.1.2 -Wall

The -Wall means to display all warnings.

Sometimes the compiler registers a warning because it thinks you did something wrong, but it doesn't break the build command.

So in theory, you could still built the executable, but it's safe to always look at these warnings and try to fix them because typically, there's an error in your program.



### 1.1.3  -fmax-errors=10

Then this -fmax-errors here, that tells the compiler well, after 10 errors, stop, stop compiling and throwing more errors because I'll get overwhelmed.



### 1.1.4 -Wextra

And the -Wextra means extra warnings that are not included yet in the w all will also be displayed.



### 1.1.5 -o

I'm going type GCC minus O program that specifies the name of the output file.

Minus O stands for output file name so program is my executable.



### 1.1.6 ./program

program是program.c编译后的结果。

./program可以执行该程序。



### 1.1.7 如果没有指定output file name

let's simply type GCCprogram.C. Let's see what happened.

There was a file now called a.out.

That is actually my executable program.



### 1.1.8 C语言程序的执行过程

Now, let me show you what actually happens behind the scenes when you call GCC.

The first thing that happens is the preprocessor is called, which means it's a simple textual replacement. For example, the contents of scdio.h is found, which is a text file, and it's actually **verbatim copied into your source code**.

(There are other things that the preprocessor does, but we're not going to go into those details.)

Next, the source code is translated into machine language into a so-called **object file**. That object file in and of itself cannot be executed. But it is the binary computer readable version of your code.

And we can force that only that step happens by typing GCC. Again, we want to specify the output file name program.o, but now I want to stop at the object face program.c 

This is what we normally would have typed.

We now, in addition to that, give the compiler an option **-c**. This flag, **-c**, tells the compiler I only want to translate into machine language.

I do not yet want to create an executable program.

So when I run this GCC command, and now I type ls, there is a **program.o** and along with my program.c. But **I can't run that**.

You can see that because it didn't change color, but if I tried to run it, permission denied.

It doesn't work, and if I try to look at it, it is a bunch of gibberish. It is the **machine language version of my program**.



So GCC again.
I want to specify the name of my output file.

```
gcc -o program program.o
```



This time, I want to create my program.
And what I want to stick into GCC is program.o because I already have this object file.

And now, when I type ls, this executable program exists.

And when I run that, it does my average seven day temperature. So the compiler really does a number of things.

It calls the preprocessor, then it translates your code into** a language the computer can actually read**. And that is then taken by the linker, which **creates the executable program**.

So now you know how to separately compile and link your code into an executable program.

This is necessary in understanding how to split your source code up over multiple source files.

That's what we'll talk about next.



## 1.4 Object file

```
touch weatherstats.c
```



将program.c中的weatherstats相关内容，剪切给weatherstats.c。



```
gcc -c weatherstats.o weatherstats.c
```

生成weatherstats.o



但因为调用了weatherstats.h

```c
#include <weatherstats.h>
```



所以gcc语句也要有所表示：

```
gcc -o program program.o weatherstats.o
```



## 1.5 Activity : Linking

Here is where we left off after the previous video: We have three files, namely program.c, weatherstats.c and weatherstats.h.

```c
// program.c

#include <stdio.h>
#include "weatherstats.h"

int main(void) {
	double temperatures[7] = {6.9, 12.3, 9.0, 5.3, 9.8, 1.8, 0.3};
	double average = averageTemp(temperatures, 7);
	printf("Average 7-day temp: %.2lf\n", average);
	return 0;
}
// weatherstats.h:

double averageTemp(double *temps, int numOfTemps);
// weatherstats.c:

double averageTemp(double *temps, int numOfTemps) {
	double result = 0.0;
	int i;

	for (i=0; i<numOfTemps; i++) {
		result = result + temps[i];
	}

	result = result / (double) numOfTemps;
	return result;
}
```

You will need these files in Weblinux, so if you have not yet created and compiled them, please do so now.

Reminder:

compile program.c to program.o using

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c program.c -o program.o
```

compile weatherstats.c to weatherstats.o using

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c weatherstats.c -o weatherstats.o
```

link program.o and weatherstats.o into executable using

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra weatherstats.o program.o -o program
```

Create a new file myNewProgram.c with the following C-code:

```c
// myNewProgram.c

#include <stdio.h>
#include "weatherstats.h"

int main(void) {
    int N = 10;

    double temperatures[] = {60, 71.5, 88, 55.5, 49, 33.5, 32, 44.5, 49.0, 50};
    double average = averageTemp(temperatures, N);
    printf("Average %d-day temp: %.2lf\n", N, average);

    return 0;
}
```

Compile myNewProgram.c into an object file myNewProgram.o using

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c myNewProgram.c -o myNewProgram.o
```

Now try the following incorrect link command:

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra myNewProgram.o program.o -o myNewProgram
```



**习题：**

（在macbook上运行即可，WebLinux有问题。）

1. Copy and paste the second line of the long error message you receive (this line starts program.c: ) into the textbox below. Do not add any spaces before or after the text.

```

```

（未完成，因为用的不是WebLinux。下面已找到正确做法，这个错误信息无伤大雅。）



2. Now correctly link myNewProgram.o and weatherstats.o to an executable myNewProgram. How do you run myNewProgram? Type the commend to **run myNewProgram** in the textbox below.

```
./myNewProgram
```



3. What is the output you receive when running myNewProgram? **Copy the exact output you receive into the textbox below.** Do not add any spaces before or after the output.

```
Average 10-day temp: 53.30
```



## 1.7 Modify object files

```
gcc -Wall -c -o program.o program.c
gcc -Wall -c -o weatherstats.o weatherstats.c
gcc -Wall -o program program.o weatherstats.o
./program
```



输出：

```
Average 7-day temp: 6.49
Highest temp: 12.30
```



修改program的内容后，重新编译并执行（weatherstats.o不需要重新编译了）

```
gcc -Wall -c -o program.o program.c
gcc -Wall -o program program.o weatherstats.o
./program
```

输出：

```
Average 7-day temp: 7.91
Highest temp: 15.30
```



## 1.8 Activity: Super Image Project

You are teaching how to compile C programs and want to share your knowledge on creating and linking object files.

You have created a file with multiple functions to apply special effects to image files.

The source code for these functions is in a file named `image.c`. You want to create an object file from this file so that it can be used in multiple projects.

You then want to use these image functions in a "superimage" project  to show some examples! The source code of this example project is in `superimage.c` and the executable file is to be called `superimage`. 



**习题：**

1. What is the necessary compilation command to create an object file `image.o` from the source file `image.c`? Type your answer in the box below. Be sure to explicitely include the name of the output file using the -o option.

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c image.c -o image.o
```



2. What is the necessary compilation command to create an object file  superimage.o from the source file superimage.c? Type your answer in the  box below. Be sure to explicitely include the name of the output file using the -o option.

 ```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c superimage.c -o superimage.o
 ```



3. What is the necessary compilation command to link these object files together into your "superimage" project?

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra image.o superimage.o -o superimage
```



# 2 Creating and using a Makefile

## 2.1 Makefile

### 2.1.1 Makefile的内容

Makefile，将前文的“先生成weatherstats.o和program.o，再生成可执行程序program”的步骤，打包。



Makefile的内容，有严格的格式；文件名，也是固定的“Makefile”。（下面的是TAB，不是空格）

```m
target (what is to be produced): what is needed to do so
	how to produce
	
program: program.o wheatherstats.o
	gcc -std=c11 -Wall -fmax-errors=10 -Wextra weatherstats.o program.o -o program
	
program.o: program.c wheatherstats.h
	gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c program.c -o program.o
	
wheatherstats.o: wheatherstats.c
	gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c weatherstats.c -o weatherstats.o
```



运行这个文件，可以在WebLinux的左边窗口的“build cmd”命令行，输入make命令；“exec”命令行，保留“./program”；再按下“run”按钮。



### 2.1.2 更改程序内容，重新执行make命令

如果在weatherstats.c中加入Minimum Temperature函数，则要在wheatherstats.h中加入相应的header（就是已经定义的函数的declaration）。program.c想要调用该函数，也得call这个函数。



这时，在terminal中，输入**make**，即可执行Makefile，不需要辛辛苦苦打3句gcc了。



### 2.1.3 Makefile很智能

如果只将program.c中的lowest temp改为lowest temperature，不更改weatherstats.c，那么，make命令非常智慧，能够识别出没有真正的改动。



所以，输入**make**命令，只会输出/执行```gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c program.c -o program.o```和```gcc -std=c11 -Wall -fmax-errors=10 -Wextra weatherstats.o program.o -o program```



## 2.4 More elaborate Makefile

更复杂版本的Makefile：

```m
# define the C compiler to use
CC = gcc
# define compiler flags
CFLAGS = -std=c11 -Wall -fmax-errors=10 -Wextra
# define library paths in addition to /usr/lib
LFLAGS = 
# define libraries to use
LIBS = 
# define the object files that this project needs
OBJFILES = program.o weatherstats.o
# define the name of thhe executable file
MAIN = program

# all of thhe below is generic - one typically only adjusts the above

all: $(MAIN)

$(MAIN): $(OBJFILES)
	$(CC) $(CFLAGS) -o $(MAIN) $(OBJFILES)
	
%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $<
	
clean:
	rm -f $(OBJECTS) $(MAIN)
```



1. So in this Makefile we first of all notice that there are comments. Anything that starts with a pound sign, that whole line becomes a comment. And so you can comment your Makefile.

2. In the next line, line two, we define which compiler to use. Because not every system will have the GCC, the new C compiler, installed. And so that's why there's a line here, GCC for my C compiler.



3. Next I define all my compiler flags.

4. There is the C11 standard for my C. There is the display all warnings, stop at 10 error messages, and display all extra warnings. So these are the flags that we want to use with a C compiler.



5. Then I left two blank lines here, one for additional library paths in addition to the regular library path. We'll add that later once we talk about libraries, and then also, what libraries to use in this project. **For now, that's nothing.** Because we're not using any additional libraries other than standard ones.



9. Next we define the object files that this project needs.

10. And it's program.o and weatherstats.o in the case of our weather program.



11. And finally, name of the executable program file,
12.  we called it program. But you could call it something else here if you didn't want the output to be called program.



14. Now anything that follows below this line is completely generic and something you wouldn't change. So if you wanted to use this Makefile for a different project, all you have to do is update things at the top.
And most likely, you would only update lines 10 and 12, and a little bit later once we do a library, maybe also the two previous ones.



16. So my first target is called All. And it dependents on dollar Main. What does that mean?This is a way to refer to variables in a Makefile Main is a variable whose content is program. And by dollar Main, I just refer to program. So it says All, the target All, depends on program.



18. Program itself depends on my object files. The object files for program that o and weatherstats.o. 

19. And to build the program, I run my compile command. So in my case, that's GCC. I add in the compiler flags, the output file name, and then the name of the object files. And we had a very similar line before in our Makefile. Just this one is more generic. And we can more easily make changes.



21. Next comes a line that tells me how to build a file with the extension .o from the same file with the extension .c.

22. we invoke the compiler with all the flags. We only want to compile because we want to go from .c to .o.
    And the name of the output file is a funny construct here. The name of the output file is given by what's in front of the colon, so whatever file came in with an extension .o. And the name of the source file is referred to in this funny way, with a dollar less than sign. That refers to the file that's to the right of the colon. So this is some funny notation you need to copy that.



24. And finally, I added a clean target in case you want to get rid of all the .o files as well as the Main program file for demonstration purposes or just to clean up. Because you only need to **keep your .c, your source files and your header file, in order to be able to rebuild your project at any time**.

25. So again, I'm starting from a clean slate.



```
~ $ ls
Makefile program.c weatherstats.c weatherstats.h

~ $ make
gcc -std=c11 -Wall -fmax-errors=10 -Wextra program.o weatherstats.o -o program
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c program.c -o program.o
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c weatherstats.c -o weatherstats.o

~ $ ./program
Average 7-day temp: 7.91
Highhest temp: 15.30
Lowest temperature: 0.30

~ $ ls
Makefile program.c weatherstats.c weatherstats.o pragram pragram.o weatherstats.h

~ $ make clean
rm -f pragram.o weatherstats.o program

~ $ ls
Makefile program.c weatherstats.c weatherstats.h
```



## 2.5 Run a program with Makefile

```m
program: program.o wheatherstats.o
	gcc -std=c11 -Wall -fmax-errors=10 -Wextra weatherstats.o program.o -o program
	
program.o: program.c wheatherstats.h
	gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c program.c -o program.o
	
wheatherstats.o: wheatherstats.c
	gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c weatherstats.c -o weatherstats.o
	
launch: program
	./program
```



在terminal中输入make launch：

```
~ $ make launch
./program
Average 7-day temp: 7.91
Highhest temp: 15.30
Lowest temperature: 0.30
```



如果修改program.c中的一个数值，那么会有重新编译program.c，重新生成program：

（weatherstats.c无需重新编译，因为其内容没有修改。）

```
~ $ make launch
gcc -std=c11 -Wall -fmax-errors=10 -Wextra weatherstats.o program.o -o program
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c weatherstats.c -o weatherstats.o
./program
Average 7-day temp: 6.49
Highhest temp: 12.30
Lowest temperature: 0.30
```



# 3 Creating a static Library

## 3.1 Create your library

### 3.1.1 Static library creation

1. compile files containing functions to object files (.o).
2. bundle these object files into an archice (.a)
3. link the library to your code containing the main function



### 3.1.2 ar命令的使用

#### 3.1.2.1 准备好.o文件

已知，program.c可生成可执行程序；而这个weatherstats.c只包含函数，不能生成可执行程序。

```
~ $ gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c weatherstats.c -o weatherstats.o
```



#### 3.1.2.2 ar命令

```
~ $ ar rcs libweather.a weatherstats.o
```



#### 3.2.2.3 ar命令详解

1. **ar**命令，有3个参数：r、c、s

R stands for replace, in case a certain .o file is already part of your library. You could replace it if you wanted to.

C stands for creative, doesn't exist yet. 

S means create an index for faster access.

We will always choose these parameters, they're very standard.



2. library的命名

以lib开头，本例为libweather，后缀为.a（as in a for this archive command）



3. 设置.o文件

即，weatherstats.o



#### 3.2.2.4 生成.a文件

```
~ $ ls *.a
libweather.a
```



### 3.1.3 library的使用

#### 3.1.3.1 用法1：libweather.a

目前已有program.o了，无需再编译了

```
~ $ gcc -o grogram program.o libweather.a
```



于是，成功生成可执行程序program。



#### 3.1.3.2 用法2：-lweather

```
~ $ rm program
~ $ gcc -o grogram program.o -L. -lweather
```



-lweather中，l代表lib，weather是library的名字。

此外，因为这个library是自己的library，并不包含在标准库的路径中。所以加入大写的L，”.“代表当前路径，L和“.”之间没有空格。



这样同样生成了可执行程序program。



### 3.1.4 dynamic or shared library

前文的是static library，是一系列object files的集合。



但还有另一种library，即dynamic or shared library。



**Static Versus Dynamic Library in C **

|Static |Dynamic |
| ---- | ---- |
| Linker fields all used library functions (such as printf(), sqrt(), etc) and copies them into your executable file. | Linked dynamically at run-time by the OS: every program that accessed the library uses the same copy. |
| Libraries have the extension .a (Linux) or .lib (Windows). | Libraries have the extension .so (Linux) or .dll (Windows). |
| Executable is a larger file, needing more disk space and main memory. | Executable only contains the name of (a link to) the library. |
| If library changes, the executable does not automatically update - needs to be re-linked. | If library changes, the executable will automatically use thhe new library code. |
| Library access is faster. | Dynamic querying of symbols takes time. |



**Static Versus Dynamic Library in C (Linux OS)**

| Library | Static | Dynamic |
| ---- | ---- | ---- |
| Compile library files | gcc -c part1.c -o part1.o <br> gcc -c part2.c -o part2.o <br> ... | gcc -c **-fpic** part1.c -o part1.o <br> gcc -c **-fpic** part2.c -o part2.o <br> ... |
| Create library | **ar rcs** libmylib.**a** part1.o part2.o ... | gcc **-shared** -o libmylib.**so** part1.o part2.o ... |
| Compile main program | gcc -c program.c -o program.o | gcc -c program.c -o program.o |
| Link library to main program | gcc -o program program.o -L. -lmylib | gcc -o program program.o -L. -lmylib <br>Add library path to environment varible: <br>**export LD_LIBRARY_PATH=$PWD:$LD_LIBRARY_PATH** |
| Run program | ./program | ./program |



1. -fpic


And the same is true for the dynamic library, but we need to add an extra compiler flag.

That compiler flag is called pic, as in **position independent code**. So the extra compiler flag is **-fpic**, because we need to create a special object file with position independent code for the dynamic linking to work properly later.



2. export LD_LIBRARY_PATH=$PWD:$LD_LIBRARY_PATH

目前的LD_LIBRARY_PATH，赋值为当前目录$PWD，加上原来的library目录。



## 3.2 Activity: create your library

![image-20200426001021244](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200426001021244.png)



## 3.4 Modify your library

```
~ $ ls
Makefile program.c weatherstats.c weatherstats.h
~ $ gcc -c weatherstats.c -o weatherstats.o
~ $ ar rcs libweather.a weatherstats.o
~ $ touch weatherio.c
~ $ touch weatherio.h
~ $ gcc -c weatherio.c -o weatherio.o
~ $ ls
Makefile program.c weatherstats.c weatherstats.h weatherstats.o libweather.a weatherio.c weatherio.o weatherio.h
~ $ ar rcs libweather.a weatherstats.o weatherio.o
~ $ touch weather.h
~ $ gcc program.c -L. -lweather -o program
~ $ ./program
```



3. 生成weatherstats.c的object文件weatherstats.o。（无法生成可执行程序，因为weatherstats.c中不含main函数。）



3. 生成library：libweather.a


5. 生成新文件weatherio.c：I've written here a simple function to print out the temperatures that are stored in the temperatures array. So my function is named Print Temperatures. It doesn't return anything. So it has a void return type. I pass to it a pointer to the temperatures array as well as the number of temperatures stored in this array. I print out over the past so-and-so many days the temperatures were. So-and-so many is, of course, the number of temperatures that was passed into this function. And then I have a simple loop that runs from i equals 0 to number of temperatures minus 1, and prints out what the temperature was on day i. Now I want this to look nice. So I want to say, on day one the temperature was, on day two the temperature was. But my i starts counting at 0. And so this person D here that indicates the day, I'm going to print out i plus 1 instead of i. And then the temperature itself, which I print out as a double with two decimal places, I use temps of i. So it's a very simple function. I'm going to save that.
6. 生成新文件weatherio.h，包含a prototype for the Print Temps function.
7. 生成weatherio.c的object文件weatherio.o。




10. 原library文件libweather.a进行拓展，既包含原来的weatherstats.o，又包含新的weatherio.o
11. 新建weather.h，写入内容如下，这样weather.h就将weatherstats.h和weatherio.h打包了：

```c
#include "weatherstats.h"
#include "weatherio.h"
```

program.c中，原来的```#include "weatherstats.h"```，此处则改为```#include "weather.h"```



12. 理论上，接下来就可以用program.c生成program.o；再用gcc把program.o和library连接起来，生成可执行程序program。但有更快的步骤，gcc之后不加-c，直接用program.c到可执行程序：

```
gcc program.c -L. -lweather -o program
```



13. program程序没有问题



## 3.5 Activity: Modify your library

library变化了。

如果原程序不修改，不会出问题，只是会按原来的操作继续做而已。

![image-20200426005529882](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200426005529882.png)



## 3.7 Ultimate makefile

### 3.7.1 回顾Makefile

这是本节2.5的内容：

```m
program: program.o wheatherstats.o
	gcc -std=c11 -Wall -fmax-errors=10 -Wextra weatherstats.o program.o -o program
	
program.o: program.c wheatherstats.h
	gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c program.c -o program.o
	
wheatherstats.o: wheatherstats.c
	gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c weatherstats.c -o weatherstats.o
	
launch: program
	./program
```



### 3.7.2 更新的结果

```m
program: program.o
	gcc -std=c11 -Wall -fmax-errors=10 -Wextra program.o -L. -lweathher -o program
	
program.o: program.c
	gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c program.c -o program.o
	
launch: program
	./program
```



在terminal中，输入：

```
make launch
```

即可运行程序program。



### 3.7.3 复杂版本的Makefile



```m
# define the C compiler to use
CC = gcc
# define compiler flags
CFLAGS = -std=c11 -Wall -fmax-errors=10 -Wextra
# define library paths in addition to /usr/lib
LFLAGS = -L.
# define libraries to use
LIBS = -lweather
# define the object files that this project needs
OBJFILES = program.o 
# define the name of thhe executable file
MAIN = program

# all of thhe below is generic - one typically only adjusts the above

all: $(MAIN)

$(MAIN): $(OBJFILES)
	$(CC) $(CFLAGS) -o $(MAIN) $(OBJFILES) $(LFLAGS) $(LIBS)
	
%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $<
	
launch: program
	./program
	
clean:
	rm -f $(OBJECTS) $(MAIN)
```



同样，在terminal中，输入：

```
make launch
```

即可运行程序program。