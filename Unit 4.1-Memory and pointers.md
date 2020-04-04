# 1 Defining and dereferencing pointers

## 1.1 The stack: visualize what happens in memory

1. 最简单的赋值

```c
#include <stdio.h>
int main(void) {
    //! showMemory(start=65520)
    int i;
    double a,b;
    char c;
    int ar[3];
    a = 1.0;
    c = 'p';
    for (i=0; i<3; i++) {
        ar[i] = i*i+1;
    }
    return(0);
}
```



2. 调用函数

```c
#include <stdio.h>
double myFunction(int, double, char);
int main(void) {
    //! showMemory(start=65520)
    int i;
    double a,b;
    char c;
    int ar[3];
    a = 1.0;
    c = 'p';
    for (i=0; i<3; i++) {
        ar[i] = i*i+1;
        b = myFunction(i, a*i, c);
    }
    return(0);
}

double myFunction(int j, double d, char l) {
    printf("Function received %d, %lf and %c.\n", j, d, l);
    j++;
    d = j*d;
    l = 'b';
    printf("In function: changed values to %d, %lf, %c.\n", j, d, l);
    return d;
}
```



## 1.2 Find the address of a variable

```c
#include <stdio.h>
void myFunction(int *, double *, char *);
int main(void) {
    //! showMemory(start=65520)
    int i = 42;
    int *iAdr = &i;
    double a = 3.14;
    double * aAdr = &a;
    char c = 'p';
    char * cAdr;
    cAdr = &c;
    printf("i = %d and its address is %p.\n", i, iAdr);
    printf("a = %lf and its address is %p.\n", a, aAdr);
    printf("c = %c and its address is %p.\n", c, cAdr);
    myFunction(iAdr, aAdr, cAdr);
    return(0);
}

void myFunction(int *iptr, double * aptr, char * cptr) {
    printf("Function receied addresses %p, %p and %p.\n", iptr, aptr, cptr);
}
```



输出：

```
i = 42 and its address is fffc.                                                 
a = 3.140000 and its address is fff0.                                           
c = p and its address is ffeb.                                                  
Function receied addresses fffc, fff0 and ffeb. 
```



## 1.3 Dereference a pointer

```c
#include <stdio.h>
int main(void) {
    //! showMemory(start=65520)
    int i = 42;
    int * iAdr; 
    double a = 3.14;
    double * aAdr = &a;
    char c = 'p';
    char * cAdr = &c;
    iAdr = &i; // alternatively int * iAdr = &i;
    printf("Address of i is %p and i = %d.\n", iAdr, *iAdr);
    printf("Address of a is %p and a = %lf.\n", aAdr, *aAdr);
    printf("Address of c is %p and c = %c.\n", cAdr, *cAdr);
    *iAdr = 50;
    printf("Address of i is %p and i = %d.\n", iAdr, i);
    *aAdr = 2.1718;
    printf("Address of a is %p and a = %lf.\n", aAdr, a);
    *cAdr = 'B';
    printf("Address of c is %p and c = %c.\n", cAdr, c);

    return(0);
}
```



输出：

```c
Address of i is fffc and i = 42.                                                
Address of a is fff0 and a = 3.140000.                                          
Address of c is ffeb and c = p.                                                 
Address of i is fffc and i = 50.                                                
Address of a is fff0 and a = 2.171800.                                          
Address of c is ffeb and c = B.
```



注意：

定义处，可以“int \* iAdr”，也可以写作“int \*iAdr”，这里的变量是iAdr，类型是int \*；

后文的“\*iAdr = 50;”，变量是\*iAdr，代表着pointer iAdr对应的原变量i。



# 2 Using pointers with functions

## 2.1 Pass pointers to functions

1. 函数中的变量值改变，不改变main中的值。

```c
#include <stdio.h>
void timesTwo(int);
int main(void) {
    //! showMemory(start=65520)
    int n;
    printf("Please enter an integer: ");
    scanf("%d", &n);
    printf("In main: You entered %d.\n", n);
    timesTwo(n);
    printf("In main: The value of n is %d.\n", n);
    return 0;
}

void timesTwo(int num) {
    printf("In the function: the number is %d.\n", num);
    num = num * 2;
    printf("In the function: the new number is %d.\n", num);
}
```



输出：

```
Please enter an integer: 42                                                     
In main: You entered 42.                                                        
In the function: the number is 42.                                              
In the function: the new number is 84.                                          
In main: The value of n is 42.  
```



2. 改成pointer，则可以改变main中变量的值

```c
#include <stdio.h>
void timesTwo(int *);
int main(void) {
    //! showMemory(start=65520)
    int n;
    printf("Please enter an integer: ");
    scanf("%d", &n);
    printf("In main: You entered %d.\n", n);
    timesTwo(&n);
    printf("In main: The value of n is %d.\n", n);
    return 0;
}

void timesTwo(int * numptr) {
    printf("In the function: the number is %d.\n", *numptr);
    *numptr = *numptr * 2;
    printf("In the function: the new number is %d.\n", *numptr);
}
```



输出：

```
Please enter an integer: 42                                                     
In main: You entered 42.                                                        
In the function: the number is 42.                                              
In the function: the new number is 84.                                          
In main: The value of n is 84. 
```



## 2.2 Pass variables to functions by reference

```c
#include <stdio.h>
void add(int, int, int *);
int main(void) {
    //! showMemory(start=65520)
	int a, b, sum;
	printf("Please enter two integers: ");
	scanf("%d%d", &a, &b);
	add(a, b, &sum);
	printf("%d + %d = %d\n", a, b, sum);
    return 0;
}

void add(int x, int y, int *resultptr) {
    int z;
    z = x+y;
    printf("Added numbers in the function!\n");
    *resultptr = z;
    printf("Updated variable with pointer in function.\n");
}
```



输出：

```
Please enter two integers: 3 5                                                  
Added numbers in the function!                                                  
Updated variable with pointer in function.                                      
3 + 5 = 8  
```



# 3 Working with pointer arithmetic

## 3.1 Pointer arithmetic

1. array包含地址信息

"int array[] = {6, 2, -4, 8, 5, 1};

printf("Array is %d.\n", array);"会给出错误提示：

```
/user-input:8:30: warning: format specifies type 'int' but the argument has type 'int *'
    printf("Array is %d.\n", array);
```

这是因为：array本身，是integer的pointer；array本身，包含了array的address信息。



正确程序为，将%d改为%p：

```c
#include <stdio.h>
int main(void) {
    //! showMemory(start=65520)
    int array[] = {6, 2, -4, 8, 5, 1};
    
    printf("Array contains %d, %d, ... , %d\n", array[0], array[1], array[5]);
    printf("These are stored at %p, %p, ..., %p\n", &array[0], &array[1], &array[5]);
    printf("Array is %p.\n", array);
    return 0;
}
```



输出：

```
Array contains 6, 2, ... , 1                                                    
These are stored at ffe8, ffec, ..., fffc                                       
Array is ffe8.  
```



2. array equals &array[0]

```c
#include <stdio.h>
int main(void) {
    //! showMemory(start=65520)
    int array[] = {6, 2, -4, 8, 5, 1};
    int *ptr, *ptr2;
    
    printf("Array contains %d, %d, ... , %d\n", array[0], array[1], array[5]);
    printf("These are stored at %p, %p, ..., %p\n", &array[0], &array[1], &array[5]);
    // array equals &array[0]
    ptr = array;
    ptr2 = &array[0];
    
    return 0;
}
```



ptr和ptr2等价



3. 如果”ptr = array;“，则*ptr和array等价；ptr++，对应着array中下一位元素的adress。

```c
#include <stdio.h>
int main(void) {
    //! showMemory(start=65520)
    int array[] = {6, 2, -4, 8, 5, 1};
    int *ptr, *ptr2;
    
    printf("Array contains %d, %d, ... , %d\n", array[0], array[1], array[5]);
    printf("These are stored at %p, %p, ..., %p\n", &array[0], &array[1], &array[5]);
    // array equals &array[0]
    ptr = array;
    ptr2 = &array[0];
    
    *ptr = 10;
    *(ptr + 1) = 5; 
    *(ptr + 2) = -1;
    
    *array = 3;
    *(array + 1) = 10;
    *(array + 2) = 99;
    
    ptr++;
    *ptr = 7;
    
    ptr += 3;
    *ptr = 8;
    return 0;
}
```



## 3.2 Activity: pointer arithmetic

2. 

![image-20200402020001856](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200402020001856.png)



正确答案：D。

因为*number等于4，4+4=8。



3. 

![image-20200402015310173](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200402015310173.png)



正确答案：E



# 4 Passing arrays to functions

## 4.1 Pass arrays to functions

1. ”printf("%d ", *(ptr+i));“等价于”printf("%d ", ptr[i]);“，尽管此处ptr的类型是int \*。

```c
#include <stdio.h>
void printArray(int *, int);
int main(void) {
    //! showMemory(start=65520)
    int array[] = {6, 2, -4, 8, 5, 1};
    int N = 6;
    printArray(array, 6);
    return 0;
}

void printArray(int * ptr, int size) {
    int i;
    for (i=0; i<size; i++) {
        // printf("%d ", *(ptr+i));
        printf("%d ", ptr[i]);
    }
    printf("\n");
}
```



2. ptr[i]等于array[i]

```c
#include <stdio.h>
void printArray(int *, int);
void squareArray(int *, int);
int main(void) {
    //! showMemory(start=65520)
    int array[] = {6, 2, -4, 8, 5, 1};
    int N = 6;
    printArray(array, 6);
    squareArray(array, 6);
    printArray(array, 6);
    return 0;
}

void squareArray(int * ptr, int size) {
    int i;
    for (i=0; i<size; i++) {
        ptr[i] = ptr[i]*ptr[i];
        // *(ptr+i) = (*(ptr+i))*(*(ptr+i));
    }
}

void printArray(int * ptr, int size) {
    int i;
    for (i=0; i<size; i++) {
        // printf("%d ", *(ptr+i));
        printf("%d ", ptr[i]);
    }
    printf("\n");
}
```



输出：

```c
Terminal
6 2 -4 8 5 1                                                                    
36 4 16 64 25 1 
```



## 4.2 Activity: arrays and functions

You are participating in a game in which players  collect points for various solved puzzles. In the end, the player with  the highest score wins. You would like to know how far behind the  highest-scoring person everyone else is in order to know whether you  still have a chance at winning. 

Please write a C program that uses a function  "behind()" (which you also have to write) in order to help with this  task. Your program should first read, from the user input, the number of players participating in the game. There are never more than 10 players in the game. Next, your program should read the current scores of each  player and store them in an array. Then you should call the function  behind(), to which you pass as a first argument, the array holding the  player's scores, and as a second argument the number of players in the  game. The function behind should replace the scores stored in the array  with the number of points by which each individual player is behind the  top-scoring player.

To help you out, the main function of the program  has already been written, so your job is simply to write the function  behind(), whose protype is also given to you.

### Provided code

```c
#include <stdio.h>

void behind(int *, int);

int main(void) {
    int array[10];
    int N, i;
    
    scanf("%d", &N);
    for (i=0; i<N; i++) {
        scanf("%d", &array[i]);
    }
    behind(array, N);
    for (i=0; i<N; i++) {
        printf("%d\n", array[i]);
    }
    
    return 0;
}

/* Write your function behind() here: */
```

### Example

#### Input

```
5                                                                               
8 12 7 15 11                                                                    
```

#### Output

```
7                                                                               
3                                                                               
8                                                                               
0                                                                               
4                                                      
```



我的程序：

```c
#include <stdio.h>

void behind(int *, int);

int main(void) {
    int array[10];
    int N, i;
    
    scanf("%d", &N);
    for (i=0; i<N; i++) {
        scanf("%d", &array[i]);
    }
    behind(array, N);
    for (i=0; i<N; i++) {
        printf("%d\n", array[i]);
    }
    
    return 0;
}

/* Write your function behind() here: */
void behind(int * arrayPtr, int N){
    int max = 0;
    int i;
    for (i=0; i<N; i++){
        if (arrayPtr[i] > max){
            max = arrayPtr[i];
        }    
    }
    
    for (i=0; i<N; i++){
        arrayPtr[i] = max - arrayPtr[i];
    }
}
```



