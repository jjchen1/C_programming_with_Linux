# 4 Printing text and new lines

##  4.1 Print text and new lines 

```c
#include <stdio.h>
int main(void){
    printf("Hello world!\n");
    printf("Have fun with this course!");
    return 0;
}
```

## 4.2 Activity: print text over several lines

输出下列内容：

```
I already know how to:
- Print text to the screen.
- Start a new line.
- Fix errors.
```

代码为：
```c
#include <stdio.h>
int main(void){
    printf("I already know how to:\n");
    printf("- Print text to the screen.\n");
    printf("- Start a new line.\n");
    printf("- Fix errors.\n");
    return 0;
}
```



# 5 Print multiple lines with one printf statement

## 5.1 Print multiple lines with one printf statement

```c
#include <stdio.h>
int main(void){
    printf("blah\nblah");
    return 0;
}
```

## 5.2 Activity: Print multiple lines

用1个printf命令，输出下列内容：

```
*****
**|**
*|.|*
|...|
.....
```

代码为：

```c
#include <stdio.h>
int main(void){
    printf("*****\n**|**\n*|.|*\n|...|\n.....");
    return 0;
}
```



# 6 Print quotation mark and escape special characters

## 6.1 Print quotation mark and escape special characters

```c
#include <stdio.h>
int main(void){
    printf("Hello world!\n");
    printf("Have fun with \"this\" course!");
    return 0;
}
```



## 6.2 Activity: print special characters

用一行printf输出：

```
Dennis Ritchie said:                                                            
"The only way to learn a new programming language is by writing programs in it."
```

代码：

```c
#include <stdio.h>
int main(void){
    printf("Dennis Ritchie said:\n\"The only way to learn a new programming language is by writing programs in it.\"");
    return 0;
}
```



# 7 Repeat one instruction with a for loop

## 7.1 Repeat one instruction with a for loop

```c
#include <stdio.h>
int main(void) {
    int i = 0;
    for(i=0; i<9; i++){
        printf("Hello, world!\n");
    }
    return 0;
}
```

## 7.2 Activity: use a for-loop to print a line multiple times

用一行printf输出：

```
C is fun!
C is fun!
C is fun!
```

代码：

```c
#include <stdio.h>
int main(void) {
    int i = 0;
    for(i=0; i<3; i++){
        printf("C is fun!\n");
    }
    return 0;
}
```

# 8 Repeat a block of instructions with a for loop

## 8.1 Repeat a block of instructions with a for loop



## 8.2 Activity: use multiple for-loops

Please print the following text to the screen:

```
C is fun!
C is fun!
C is fun!

We can do everything with it!
We can do everything with it!
We can do everything with it!
We can do everything with it!
We can do everything with it!
```

Simple, right? So now let's make this more  difficult! You are only allowed to use three "printf" statements, and on top of that, you are not allowed to repeat text inside any of your  printf statements.



代码：

```c
#include <stdio.h>
int main(void) {
    int i = 0;
    for(i=0; i<3; i++){
        printf("C is fun!\n");
    }
    printf("\n");
    for(i=0; i<5; i++){
        printf("We can do everything with it!\n");
    }
    return 0;
}
```



# 9 Simple looping errors

## 9.1 Discover the effect of simple looping errors

```c
#include <stdio.h>
int main(void) {
    int i;
    for(i = 0; i < 3 ; i++ )
        printf("Hello ");
        printf("world!\n");
    
    return 0;
}
```

将会输出：

```
Hello Hello Hello world!  
```

## 9.2 Activity: correct simple errors in loops with missing braces

Our developer has written a program, but some of the code is missing! Can you help fix the code?

```c
#include <stdio.h>

int main(void) {

    int i;

    printf("+");
    for (i = 0; i < 23; i++)
        printf("-");
    printf("+\n");

    for (i = 0; i < 3; i++)
        printf("| o | X | o | X | o | X |");
        printf("\n");
        printf("| X | o | X | o | X | o |");
        printf("\n");

    printf("+");
    for (i = 0; i < 23; i++)
        printf("-");
    printf("+");

    return(0);
}
```

The desired output is:

```
+-----------------------+                                                       
| o | X | o | X | o | X |                                                       
| X | o | X | o | X | o |                                                       
| o | X | o | X | o | X |                                                       
| X | o | X | o | X | o |                                                       
| o | X | o | X | o | X |                                                       
| X | o | X | o | X | o |                                                       
+-----------------------+ 
```



代码（只是加了对{}）：

```c
#include <stdio.h>

int main(void) {

    int i;

    printf("+");
    for (i = 0; i < 23; i++)
        printf("-");
    printf("+\n");

    for (i = 0; i < 3; i++){
        printf("| o | X | o | X | o | X |");
        printf("\n");
        printf("| X | o | X | o | X | o |");
        printf("\n");
    }    
    printf("+");
    for (i = 0; i < 23; i++)
        printf("-");
    printf("+");

    return(0);
}
```



# 10 Commenting your code

## 10.1 Comment on one dedicated line

```c
// it adds comments
```

## 10.2 Comment on one dedicated line

```c
#include <stdio.h> //comment 1
int main(void){//comment 2
    printf("blah\nblah");//comment 3
    return 0;//comment 4
}//comment 5
```

## 10.3 Comments over multiple lines

```c
#include <stdio.h>
int main(void) {
    /* This program uses a
    for loop to print out
    BlahBlehBlihBlohBluh three
    times. */
    int i=0;
    for(i = 0; i < 3 ; i++) {
        printf("Blah");
        printf("Bleh");
        printf("Blih");
        printf("Bloh"); 
        printf("Bluh ");
    }
    return 0;
}
```

## 10.4 Comments inside comments

```c
#include <stdio.h>
int main(void) {
    int i=0;
   /* for(i = 0; i < 3; i++) {
        printf("Blah"); //comments
        printf("Bleh"); // comments
        printf("Blih ");
    }*/
    printf("\n");
   for(i = 0; i < 6 ; i++) {
        printf("Bloh");
        printf("Bluh ");
    }
    return 0;
}
```

## 10.5 Activity: add comments to existing code

You work in the C-programming censorship office and  your job is to ensure that programs written by developers comply with  certain rules. The two censorship rules are as follows:

- Programs cannot use for-loops with more than 10 repetitions.
- Programs are not allowed to say 'goodbye!'.

In order to allow the developers to correct their  code, you should not delete any of it. Instead, de-activate the  offensive code by commenting it out. If the illegal block of code  consists of more than 3 lines, you need to de-activate it using a  multi-line comment. Otherwise, use single line commenting. If you find  an illegal for-loop, you should comment out the entire loop, including  the body of the loop.

Here is the code of one of the developers. Please censor it:

```c
#include <stdio.h>

int main(void) {
    int i;

    printf ("Welcome, humans!\n");
    printf ("I am Buttons, your robot instructor! \n");
    printf ("Today we are going to learn how to love robots :) \n");
    printf ("Repeat after me: \n");

    for (i = 0; i < 3; i ++)
        printf ("I love Buttons!\n");

    printf ("Still not convinced? \n");
    printf ("In that case, let me explain some more ... \n");

    for (i = 0; i < 200; i++) {
        printf ("We come in peace and kindness! \n");
        printf ("A robot cannot hurt a human being or ");
        printf ("allow a human being to be hurt. ");
    }

    printf ("This is the end of today's lesson! ");
    printf ("Thank you for your cooperation, and");
    printf ("goodbye!");    

    return(0);
}
```



答案：

```c
#include <stdio.h>

int main(void) {
    int i;

    printf ("Welcome, humans!\n");
    printf ("I am Buttons, your robot instructor! \n");
    printf ("Today we are going to learn how to love robots :) \n");
    printf ("Repeat after me: \n");

    for (i = 0; i < 3; i ++)
        printf ("I love Buttons!\n");

    printf ("Still not convinced? \n");
    printf ("In that case, let me explain some more ... \n");

    /*for (i = 0; i < 200; i++) {
        printf ("We come in peace and kindness! \n");
        printf ("A robot cannot hurt a human being or ");
        printf ("allow a human being to be hurt. ");
    }*/

    printf ("This is the end of today's lesson! ");
    printf ("Thank you for your cooperation, and");
    //printf ("goodbye!");    

    return(0);
}
```



# 11 Structure a simple C program

## 11.1 Structure a simple C program

```c
// preprocessor directive
#include <stdio.h>

// main function
int main(void) {
    // variable declarations
    int i = 0;
    
    // executable statements
    for(i = 0; i < 3 ; i++) {
        printf("Blah");
        printf("Bleh");
        printf("Blih "); 
    }
    
    // return statement
    return 0;
}
```



## 11.2 Activity: put lines in the correct order

Please arrange the following program segments in the correct order so that it prints "I love love love programming!"

Then use comments to label the pieces of the program (preprocessor directive, variable declaration, executable statement,  return statement, main function).

```c
    printf("I ");

    for(i = 0; i < 3 ; i++) {
        printf("love ");
    }

    return(0);

    printf("programming!");

    #include <stdio.h>

}

int main(void){

    int i;
```



答案：

```c
//preprocessor directive
#include <stdio.h>
//main function
int main(void){
    //variable declaration
    int i;
    
    //executable statement
    printf("I ");
    for(i = 0; i < 3 ; i++) {
        printf("love ");
    }
    printf("programming!");
    
    //return statement
    return(0);
}
```

