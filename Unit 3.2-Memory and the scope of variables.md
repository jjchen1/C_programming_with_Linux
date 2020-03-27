

# 1 Understanding computer memory

## 1.1 Discover the Von Neumann architecture

### 1.1.1 Princeton architecture
John von Neumann was part of a group of people who created a model that describes the insides of a computer. He was a physicist and mathematician born in 1903 in Budapest, Hungary. The von Neumann architecture, used in all modern computers,
is named after him. There still exists a controversy around the naming of this architecture,
however. John William Mauchly and John Eckert used this concept already in their work
on the big ENIAC computer.

To give a good tribute to everyone, we speak about the **Princeton architecture**.

![image-20200326131507444](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326131507444.png)

1. arithmetic logic unit (ALU)
Its role is to perform basic operations, such as plus, minus, times, division, as well as logical operations, such as and, or, and not.

2. control unit
It coordinates the operation and sequence of data movements between the other parts of the architecture.

**CPU = arithmetic logic unit + control unit**

3. memory
It serves both data and programs.
Memory comes in two flavors, temporary memory, also called **RAM**, short for random access memory, and lasting memory, such as hard drives.
4. input and output
This enables communication between the computer and the external world, such as the user, peripherals, and even other computers.

Most computers conceived of between the 1940s and the early 1970s were designed according to this model.

### 1.1.2 New ideas
As computers started evolving more rapidly in the 1970s, new ideas emerged.

For example, computer memory can now communicate directly with input and output, bypassing the CPU entirely.

![image-20200326132314526](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326132314526.png)

But let's keep it simple for now.

The architecture we just described provides a good if somewhat simplified overview of what are still the main concepts in modern computer information technology.



## 1.2 Memory representation, RAM, cells, word, byte, bit, memory address

### 1.2.1 two different types of memory

1. RAM (short for Random Access Memory)

It is temporary memorythat is easy and quick to access and, for example, used to execute programs.

We also call this type of storage volatile memory.

![image-20200326140325032](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326140325032.png)



2. nonvolatile, or lasting memory

It is for more permanent storage of data, for example, used to store files on the hard drive.

![image-20200326140335656](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326140335656.png)



### 1.2.2 memory is composed of bits and each variable has its own address

The vast majority of computer programs uses the computer's RAM during execution.
Values of variables, for example, are stored in -- meaningful written to and read from -- Random Access Memory.

For simplicity, we may represent the Random Access Memory as a sequence of binary memory cells, each populated with a 0 or a 1. 



We call each such cell **1 bit**.

By grouping several of these cells or bits together, we create what is called a word.
A word is the fundamental unit of data that can be moved between the RAM and the computer processor.
The size of a word is thus expressed in number of bits --that is, number of memory cells --or in bytes.

Recall that **1 byte equals 8 bits**.

Modern personal computers and modern processors more ordinarily tend to use **8, 16, 32, or even 64 bits** to form one word, though other word sizes are possible.

These particular word sizes emerge historically as a result of the hardware architecture, but they have evolved over time.

Why would one want to group memory cells into words?

Well, this allows for the addressing of memory.
In fact, an address is assigned to each word. We also call this a memory address. The computer address is a whole number that describes the location of the word in the computer memory.

For example, imagine the computer whose word length is 8 bits. Suppose, in addition, that this computer can store a total of four words.

It's not a very big computer. One could then address the computer's memory
by assigning an address to each of the four words, just like you would assign an address to each of four houses on a street. Each word gets a number as its address.

Look here. The address 0 would be used for the first word : that is, the first 8 memory cells.
The address 1 would be used for the second word : the next 8 memory cells.
The address 2 would be used for the third word, and the address 3 would be used for the fourth word.

In the C programming language, it is possible to get these memory addresses during the execution of a program.

For example, if I use a variable in my program that stores an integer value, then not only could I find and use this value during my program, but equally well, I could obtain the memory location - that is, the address where the value is stored.

The use of memory addresses allows low-level access to the computer by allowing direct access to the computer's memory. One could literally move through the computer's memory from word to word.

This technique allows for optimization of memory usage at a very precise level, or of performance
in terms of execution speed. This is an extremely powerful tool for application developers.

So now you know that **each variable has its own address, and that memory is composed of bits --
cells -- that are organized into words**.



## 1.3 Activity: memory management and representation

![image-20200326144407502](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326144407502.png)

正确答案：the operating system



# 2 Determining the amount of memory used for different data types

## 2.1 Get and print the size of basic types

一个char、int、double，对应的byte为：1、4、8

```c
#include <stdio.h>
int main() {
    char c;
    int i;
    double d;
    char listChar[3];
    int listInt[3];
    double listDouble[3];
    
    printf("%zu\n", sizeof(char)); //得到：1
    printf("%zu\n", sizeof(int)); //得到：4
    printf("%zu\n", sizeof(double)); //得到：8
    return(0);    
}
```



换成对应的变量，则结果不变，byte还是1、4、8：

```c
#include <stdio.h>
int main() {
    char c;
    int i;
    double d;
    char listChar[3];
    int listInt[3];
    double listDouble[3];
    
    printf("%zu\n", sizeof(c));//得到：1
    printf("%zu\n", sizeof(i));//得到：4
    printf("%zu\n", sizeof(d));//得到：8
    return(0);    
}
```



改成长度为3的array，则大小乘以3倍：3、12、24

```c
#include <stdio.h>
int main() {
    char c;
    int i;
    double d;
    char listChar[3];
    int listInt[3];
    double listDouble[3];
    
    printf("%zu\n", sizeof(listChar));//得到：3
    printf("%zu\n", sizeof(listInt));//得到：12
    printf("%zu\n", sizeof(listDouble));//得到：24
    return(0);    
}
```



## 2.4 Activity: compute space

A delivery company has hired you to manage their  tracking services division. It is your job to store all of the currently used tracking codes in the company's database. These codes consist of  either all integers, all decimal numbers, or all characters. The chief  technology officer has warned you that the database is old and has  limited space, so you want to determine how much memory the tracking  codes will occupy before storing them. You decide to write a program to  assist you in this process. 

Your program should first read an integer number  indicating how many tracking codes you plan on entering. Next, for each  successive tracking code your program should read in the integer length  of code followed by a space and then the type of code ('i' for integer,  'd' for decimal, or 'c' for character). Finally your program should  print the total amount of space required to store all of the tracking  codes (in bytes). If the user enters an incorrect type for any tracking  number, the program should print 'Invalid tracking code type' and exit.

### Examples

#### Input:

```
3
10 i
7 c
12 d 
```

#### Output:

```
143 bytes
```

 

#### Input:

```
2
3 c
20 d
```

#### Output:

```
163 bytes
```

####  

#### Input:

```
4
5 i
2 d
10 a
3 c
```

#### Output:

```
Invalid tracking code type 
```



我的程序：

```c
#include <stdio.h>
int main(void){
    int number, size, i;
    int sum=0;
    int isOK=1;
    char kind;
    scanf("%d", &number);
    for (i=0; i<number; i++){
        scanf("%d %c", &size, &kind);
        if (kind == 'c') {
            sum += size*1; 
        } else if (kind == 'i') {
            sum += size*4; 
        } else if (kind == 'd') {
            sum += size*8; 
        } else {
            printf("Invalid tracking code type");
            isOK = 0;
        } 
    }
    
    if (isOK) {
        printf("%d bytes", sum);
    }
    return 0;
}
```



## 2.6 Be aware of the largest possible value for an integer!

```c
#include <stdio.h>
int main() {
    int num = 2147483645;
    int i;
    
    for (i=0; i<8; i++) {
        printf("%d\n", num);
        num = num+1;
    }
    
    return(0);
}
```

终端输出很奇怪：

```
2147483645                                                                      
2147483646                                                                      
2147483647                                                                      
-2147483648                                                                     
-2147483647                                                                     
-2147483646                                                                     
-2147483645                                                                     
-2147483644 
```



![image-20200326173547733](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326173547733.png)



## 2.7 Round off numbers and circumvent errors

### 2.7.1 double 0.25

```c
#include <stdio.h>
int main() {
    double num = 0.25;
    
    printf("the number is %lf\n", num);
    printf("the number is %.20lf\n", num);
    printf("the number is %.40lf\n", num); 
    return(0);
}
```



得到：

```
the number is 0.250000
the number is 0.25000000000000000000
the number is 0.2500000000000000000000000000000000000000  
```



### 2.7.2 double 0.3

```c
#include <stdio.h>
int main() {
    double num = 0.3;
    
    printf("the number is %lf\n", num);
    printf("the number is %.20lf\n", num);
    printf("the number is %.40lf\n", num); 
    return(0);
}
```



得到：

```
the number is 0.300000 
the number is 0.29999999999999998890
the number is 0.2999999999999999888977697537484345957637 
```



### 2.7.3 float 0.3

```c
#include <stdio.h>
int main() {
    float num = 0.3;
    
    printf("the number is %.40f\n", num); 
    return(0);
}
```



结果误差更大了：

```
the number is 0.3000000119209289550781250000000000000000 
```



### 2.7.4 float 0.25

```c
#include <stdio.h>
int main() {
    float num = 0.25;
    
    printf("the number is %.40f\n", num); 
    return(0);
}
```



0.25换成float格式后，不受影响，还是很准确：

```
the number is 0.2500000000000000000000000000000000000000 
```



### 2.7.5 0.25和0.3的区别

因为在计算机中，数据以0和1存储，所有都需要二进制（binary system），即2的n次方。

0.25=1/4=2<sup>-2</sup>，在计算机中，可以很准确地表达。

而0.3是由多个不同的2<sup>-n</sup>组成的，就没有那么准确。



## 2.8 Activity: memory usage displayed

You are programming a toaster! The toaster does not  have a lot of memory, so you need to be careful about the data types you use (remember that different data types use different amounts of  memory). To make this easier, you'd like an easy way to track how much  memory your variables are going to use.

Your job is to write a program that shows, in  human-readable form (see below for specifics), how much memory a set of  variables of a certain type will use. Your program should read a  character that identifies the data type ('i' for int, 's' for short, 'c' for char, 'd' for double). Next it should read an integer that  indicates how many variables of the given type you wish to store.

Your program should then calculate the amount of  memory required to store the given variables. Your program needs to be  written in such a way that it would also perform correctly on other  computers. In other words, rather than hard-coding specific sizes for  the different variable types, your program needs to use the "sizeof()"  function to determine how much memory an individual variable of a given  type needs.

Finally, you need to output the amount of space  required by your variables to the screen. You need to make sure you  provide this output in a form that is easy to read for humans. The  following examples illustrate what this means:

### Examples

If the user input were:

```
i 36794
```

then the amount of space needed (if we assume that  an integer uses 4 bytes in memory) would be 4*36794 = 147176 bytes. This corresponds to 147 kilobytes and 176 bytes, so the output should be:

```
147 KB and 176 B
```

 

#### Input:

```
d 654250
```

#### Output:

```
5 MB and 234 KB and 0 B
```

 

#### Input:

```
d 35
```

#### Output:

```
280 B
```



我的程序：

```c
#include <stdio.h>
int main(void){
    int sizeInt, sizeShort, sizeChar, sizeDouble;
    int number, size;
    char kind;
    
    scanf("%c %d", &kind, &number);
    
    sizeInt = sizeof(int); 
    sizeShort = sizeof(short); 
    sizeChar = sizeof(char); 
    sizeDouble = sizeof(double); 

   if (kind == 'i') {
        size = number * sizeInt; 
    } else if (kind == 's') {
        size = number * sizeShort; 
    } else if (kind == 'c') {
        size = number * sizeChar; 
    } else if (kind == 'd') {
        size = number * sizeDouble; 
    } else {
        size = 0;
    }
    
    if (size/1000000 > 0) {
        printf("%d MB and %d KB and %d B", size/1000000, (size%1000000)/1000, size%1000);
    } else if (size/1000 > 0) {
        printf("%d KB and %d B", size/1000, size%1000);
    } else {
        printf("%d B", size);
    }    
    
    return 0;
}
```



# 3 Determining the scope of variables

## 3.1 Visualize what happens in the stack of the memory with code

```c
#include <stdio.h>
int main() {
    //! showMemory(start=65520)
    char c = '?';
    short s = 2301;
    int i = 987654;
    double d = 26.49;
    char l[5] = {'a','b','c', 'd', 'e'};
    short lShort[4] = {163, 365, 852, 1424};
    int lInt[3] = {2876, 26532, 37652};
    double lDouble[2] = {86.263, 265.2774};
    return 0;
}
```

![image-20200326184437706](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326184437706.png)



## 3.2 Scope and blocks in C: scope of variables when using blocks

```c
#include <stdio.h>
int main(){
    //! showMemory(start=65520)
    int a = 10;
    int b = 11;
    {
        int c = 12;
        int d = 13;
        int e = a + c;
        c = b + d;
        printf("c: %d\n", c);
        printf("e: %d\n", e);
    }
    int f = 14;
    int g = 15;
    printf("f: %d\n",f);
    printf("g: %d", g);
}
```

1.  内存中放入a=10和b=11

![image-20200326195243394](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326195243394.png)

2. 进入block，内存中放入c = 12，d=13，e=22

![image-20200326195134917](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326195134917.png)

3. c的值改为24

![image-20200326195056397](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326195056397.png)

4. 离开block，variable消失了，但value还是存在的

![image-20200326195401922](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326195401922.png)

5. f=14和e=15，覆盖了原来的值

![image-20200326195649649](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326195649649.png)



6. 如果将第15行的“f=14”，改为“f=c”，就会报错：

```
/user-input:15:13: error: use of undeclared identifier 'c'
    int f = c;
```

因为此时的变量c，已经被destroy了。



## 3.3 Scope and functions in C: scope of variables when using functions

main和其他block（这里是函数）的变量不通用，需要传递参数进去。parameters和arguments，变量名可以不同，但类型要相同。

```c
#include <stdio.h>
void doSomething(int);
int main(){
    //! showMemory(start=65520)
    int a = 10;
    int b = 11;
    int f = 14;
    int g = 15;
    doSomething(b);
    printf("f: %d\n",f);
    return(0);
}

void doSomething(int h)
{
        int a = 20;

        int c = 12;
        int d = 13;
        int e = a + c;
        c = h + d;
        printf("c: %d\n",c);
        printf("e: %d\n",e);
}
```

