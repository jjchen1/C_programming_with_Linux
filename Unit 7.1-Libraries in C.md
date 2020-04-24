[TOC]

# 1 Declaring and defining functions

## 1.1 Distinguish between function declaration and function definition

函数的definition，是函数整体；函数的declaration，是函数的第一句，定义了函数的参数、传出的参数类型。



（如果变量类型没定义，C默认类型是int）



如果自定义函数在main下方，则要在main之前做出函数的declaration。**两者缺一不可。**



## 1.2 Activity: function declaration versus definition

Petra lives in the United States, where temperature  is measured in Fahrenheit, whereas Rémi lives in France, where one  measures in Celsius. During their weekly meetings to discuss the  preparation of this course, they often wonder who currently has the  nicer weather.

To help with this important discussion, complete the below C program that converts temperature from Fahrenheit to Celsius or from Celsius to Fahrenheit, depending on the user's input. The user  should enter an integer, followed by a space, followed by the letter 'F' (for Fahrenheit) or the letter 'C' (for Celsius) and the program then  converts this temperature to the other unit and prints it out with one  decimal place (see examples below).

Your job is to complete the given program by filling in the function prototypes, the function calls, and the printf()  statements at the indicated locations (lines that start with //).

**Examples**

**Input:**

```
45 F
```

**Output:**

```
7.2 C
```

**Input:**

```
28 C
```

**Output:**

```
82.4 F
```

**Provided code**

```c
#include <stdio.h>

// insert prototype for function ftoc() here

// insert prototype for function ctof() here


int main(void) {

    int usertemp;
    char unit;
    double convertedtemp;

    scanf("%d %c", &usertemp, &unit);
    if (unit=='C'){
        // insert function call here to convert usertemp 
           /* from Celsius to Fahrenheit and store the result in convertedtemp */

        // complete this line to print out the conversion result

    } else if (unit=='F'){

        // insert function call here to convert usertemp 
           /* from Fahrenheit to Celsius and store the result in convertedtemp */
        
        // complete this line to print out the conversion result
        
    }

    return 0;

}

/* Function definitions below are provided for you*/

/* Conversion from Celsius to Fahrenheit: */
double ctof(int x){
    return((9.0/5)*x+32);
}

/* Conversion from Fahrenheit to Celsius: */
double ftoc(int x){
    return(5.0/9*(x-32));
}
```



**我的程序：**

```c
#include <stdio.h>

double ctof(int x);// insert prototype for function ftoc() here

double ftoc(int x);// insert prototype for function ctof() here


int main(void) {

    int usertemp;
    char unit;
    double convertedtemp;

    scanf("%d %c", &usertemp, &unit);
    if (unit=='C'){
        convertedtemp = ctof(usertemp);// insert function call here to convert usertemp 
           /* from Celsius to Fahrenheit and store the result in convertedtemp */

        printf("%.1lf F", convertedtemp);// complete this line to print out the conversion result

    } else if (unit=='F'){

        convertedtemp = ftoc(usertemp);// insert function call here to convert usertemp 
           /* from Fahrenheit to Celsius and store the result in convertedtemp */
        
        printf("%.1lf C", convertedtemp);// complete this line to print out the conversion result
        
    }

    return 0;

}

/* Function definitions below are provided for you*/

/* Conversion from Celsius to Fahrenheit: */
double ctof(int x){
    return((9.0/5)*x+32);
}

/* Conversion from Fahrenheit to Celsius: */
double ftoc(int x){
    return(5.0/9*(x-32));
}
```



# 2 Using the math library in C

## 2.1 Use the math library

### 2.1.1 libm.a

使用已有的库，只需要declaration，不需要definition了。

比如，定义pow：

```c
double pow(double, double);
```



```c
#include <stdio.h>
double pow(double, double);/*Write your C code here*/

int main(void) {
	double a = 2.5;
	double aSquared = pow(a, 2);
	printf("%d ^2 = %.2lf", a, aSquared);
	return 0;
}
```



WebLinux的build cmd中，在-o前加入libm.a的绝对路径/usr/lib/libm.a：

libm中的m代表math

libm.a is the math library for the C programming language. 

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra program.c /usr/lib/libm.a -o program
```



其他系统中，libm的后缀可能不是a，而是so



运行失败



### 2.1.2 math.h方法

也可以将/usr/include/math.h拷贝到当前目录下，可用```#include <math.h>```，此时则无需```double pow(double, double);```了

/usr/include包含所有header

```c
#include <stdio.h>
#include <math.h>

int main(void) {
	double a = 2.5;
	double aSquared = pow(a, 2);
	printf("%d ^2 = %.2lf", a, aSquared);
	return 0;
}
```



m代表math.a

gcc命令，-l代表当前目录，lib也可去掉，剩下```-l m.a```，再去掉后缀.a，结合l和m，最终为-lm

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra program.c -lm -o program
```



如果用其他的library，如libxkbfile.so，则用xkbfile取代“-lm”中的“m”



### 2.1.3 library的位置

And let's try to find where is the definition of all those math libraries.

Well, I'm going to tell you where it is installed in the system.

Usually it is in a folder called /usr/lib for libraries.

So let's go to that folder.

And I will list all the files. If I do ls, you can see that we have many, many, many libraries. So because we have many of them, let's try to put the outputs into the less command.

```
ls | less
```







## 2.2 Activity: use the math library

You are teaching a class on C-programming. The topic of your next lecture is libraries (what a coincidence!). You would like to teach about the use of the mathematics library in C. To accomplish  this, you have written a program which you intend to discuss with your  students during the next class. 

Your program should first read from the user an  integer, and next take the square root of that integer and print it out  with 8 decimal places. Next, your program should find and print out (on a new line) the mathematical constant e (Euler's constant) with 10  decimal places. To find e, use the mathematical function exp() and note  that e = exp(1).

Finally, in order to remind your students how to use the compiler, please print (on a new line) the correct compiler command to link the mathematics library with your program. Note that in the  example given below this line needs to be correctly completed. Your  program's source code si stored in program.c, and your compilation  command should produce an executable titled program.

**Example**

**Input:**

```
2
```

**Output:**

```
1.41421356                                                                      
2.7182818285                                                                    
gcc -std=c11 -Wall -fmax-errors=10 -Wextra (... you need to complete this line correctly ...)
```



**我的程序：**

```c
#include <stdio.h>
#include <math.h>

int main(void){
    int a; 
    scanf("%d", &a);
    printf("%.8lf\n%.10lf\n", sqrt(a), exp(1));
    printf("gcc -std=c11 -Wall -fmax-errors=10 -Wextra program.c -lm -o program");
    return 0;
}
```



注意，-std=c11 -Wall -fmax-errors=10还是保留着吧：

```
Use the -std flag to set the C standard (in this case c11) for your code to be compiled with.
This will warn you if you break c11 standard rules! (-3 points)

Use the -Wall flag to turn on additional warnings about potential bad code practices. (-3 points)

Use the -Wextra flag to turn on even more warnings than the -Wall flag alone will activate. (-3 points)
```



# 3 Using multiple libraries in C

## 3.1 Use multiple libraries in C

```c
#include <stdlib.h>
#include <curses.h>
#include <menu.h>
#include <stdio.h>
```



```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra program.c -lcurses -lmenu -o program
```





## 3.2 Activity: using the JPEG library

You are still teaching that unit on libraries to  your students! This time you want to demonstrate how to invoke the JPEG  library (libjpeg.so), which can be used to read and write image files in JPEG format (feel free to play around here - this is pretty neat!). 

You ask your students to write a program with source code stored in vizplus.c and which uses the JPEG library. In order to  help your students you decide to print out the compilation command for  them that creates an executable file called vizplus from vizplus.c along with linking the JPEG library during the translation process. 

Please write a program that prints the necessary  compilation command with a simple printf(). Again, your students' source code is provided in vizplus.c. You only need to link the JPEG library  and produce an executable file called vizplus.



**我的程序：**

```c
#include <stdio.h>
#include <libjpeg.so>

int main(void){
    printf("gcc -std=c11 -Wall -fmax-errors=10 -Wextra vizplus.c -ljpeg -o vizplus");
    return 0;
}
```

