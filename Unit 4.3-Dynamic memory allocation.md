[TOC]

# 1 Allocating memory at runtime

## 1.1 Allocate memory in the heap using malloc

1. 

malloc：动态内存分配

heap：堆

注意：```#include <stdlib.h>```



2. 1个malloc(4)

```c
#include <stdlib.h>
int main(void){
    //! showMemory(start=272)
    malloc(4);
    return 0;
}
```

![image-20200403132048677](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403132048677.png)

3. 2个malloc(4)

```c
#include <stdlib.h>
int main(void){
    //! showMemory(start=272)
    malloc(4);
    malloc(4);
    return 0;
}
```

![image-20200403132345260](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403132345260.png)

4. 2个malloc(1)

```c
#include <stdlib.h>
int main(void){
    //! showMemory(start=272)
    malloc(1);
    malloc(1);
    return 0;
}
```

![image-20200403132526022](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403132526022.png)

因为4bytes是最小单位，都是4的倍数；如果小于4，则显示4。



5. malloc(5)显示8bytes

```c
#include <stdlib.h>
int main(void){
    //! showMemory(start=272)
    malloc(5);
    malloc(5);
    return 0;
}
```

执行1个malloc(5)后：

![image-20200403132804997](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403132804997.png)

执行2个malloc(5)后：

![image-20200403132838980](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403132838980.png)

6. 使用sizeof()，正好得到integer、double的大小

```c
#include <stdlib.h>
int main(void){
    //! showMemory(start=272)
    malloc(sizeof(int));
    malloc(sizeof(double));
    return 0;
}
```

![image-20200403133024700](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403133024700.png)

![image-20200403133050796](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403133050796.png)

7. 几倍的size()

```c
#include <stdlib.h>
int main(void){
    //! showMemory(start=272)
    malloc(3*sizeof(int));
    malloc(4*sizeof(double));
    return 0;
}
```



3*sizeof(int)，12 bytes

![image-20200403133147327](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403133147327.png)

4*sizeof(double)，32 bytes

（图太长了，不显示了）



8. pointer

```c
#include <stdlib.h>
int main(void){
    //! showMemory(start=272)
    int * intptr;
    double * doubleptr;
    intptr = (int *) malloc(sizeof(int));
    doubleptr = (double *) malloc(sizeof(double));
    return 0;
}
```



![image-20200403134034775](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403134034775.png)

```malloc(sizeof(int)```和```malloc(sizeof(double)```的位置，从“6. 使用sizeof()，正好得到integer、double的大小”得到。



所以，intptr和doubleptr赋值为：

<img src="/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403134347829.png" alt="image-20200403134347829" style="zoom: 67%;" />

9. 给```* intptr```和```* doubleptr```赋值

```c
#include <stdlib.h>
int main(void){
    //! showMemory(start=272)
    int * intptr;
    double * doubleptr;
    intptr = (int *) malloc(sizeof(int));
    * intptr = 5;
    doubleptr = (double *) malloc(sizeof(double));
    * doubleptr = 9.0;
    return 0;
}
```

int格式的5：
![image-20200403135414417](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403135414417.png)

double格式的9.0：
![image-20200403135437330](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403135437330.png)



# 2 Freeing dynamically allocated memory

## 2.1 Deallocate memory in the heap using free

1. free()后，仍可能使用变量

```c
#include <stdio.h>
#include <stdlib.h>
int main(void) {
    //! showMemory(start=438, cursors=[a,b,c])
    int *a;
    a = (int *) malloc(sizeof(int));
    *a = 1;
    printf("I stored %d at memory location %p.\n", *a, a);
    free(a);
    printf("Can I still access a?\n");
    printf("I stored %d at memory location %p.\n", *a, a);
    return 0;
}
```

![image-20200403141846240](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403141846240.png)

```free(a);```后，1仍存在着，但存储空间不在了。



此处仍然可以打印出*a和a。但这只是因为足够幸运，有可能仍能使用被free的变量，有可能用不了。

```
I stored 1 at memory location 163.                                              
Can I still access a?                                                           
I stored 1 at memory location 163.                    
```



2. 3个变量都free()

```c
#include <stdio.h>
#include <stdlib.h>
int main(void) {
    //! showMemory(start=438, cursors=[a,b,c])
    int *a, *b, *c;
    a = (int *) malloc(sizeof(int));
    *a = 1;
    printf("I stored %d at memory location %p.\n", *a, a);
    b = (int *) malloc(sizeof(int));
    *b = 2;
    free(a);
    c = (int *) malloc(sizeof(int));
    *c = 3;
    printf("Can I still access a?\n");
    printf("I stored %d at memory location %p.\n", *a, a);
    return 0;
}
```



先释放了a的空间，后来的c，占据的是a原来占据的空间

![image-20200403142512502](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200403142512502.png)

输出了c的值，3：

```
I stored 1 at memory location 163.                                              
Can I still access a?                                                           
I stored 3 at memory location 163. 
```



3. 也可以释放所有3个变量的空间：

```c
#include <stdio.h>
#include <stdlib.h>
int main(void) {
    //! showMemory(start=438, cursors=[a,b,c])
    int *a, *b, *c;
    a = (int *) malloc(sizeof(int));
    *a = 1;
    printf("I stored %d at memory location %p.\n", *a, a);
    b = (int *) malloc(sizeof(int));
    *b = 2;
    free(a);
    c = (int *) malloc(sizeof(int));
    *c = 3;
    printf("Can I still access a?\n");
    printf("I stored %d at memory location %p.\n", *a, a);
    free(b);
    free(c);
    return 0;
}
```



# 3 Storing and addressing arrays in dynamically allocated memory

## 3.1 Allocate memory for arrays using malloc

```c
#include <stdlib.h>
int main(void) {
    //! showMemory(start=272)
    int * array;
    array = (int *) malloc(5*sizeof(int));
    array[0] = 3;
    array[1] = 44;
    array[2] = 2;
    * (array + 3) = 7;
    * (array + 4) = -1;
    free(array);
    return 0;
}
```



## 3.2 Learn from another example of array memory allocation

```c
//new example of the use of malloc
#include <stdio.h>
#include <stdlib.h>

int * allocateIntArray(int);
double findAverage(int *,int);

int main(void){
    //! showMemory(start=272)
    int num, i;
    int * array;
    double average;
    printf("How many grades would you like to enter?");
    scanf("%d",&num);
    array = allocateIntArray(num);
    printf("Please enter %d grades: ",num);
    for(i=0;i<num;i++){
        scanf("%d",array+i);
    }
    average = findAverage(array,num);
    printf("The average grade is %.2f.\n",average);
    free(array);
    return 0;
}

int * allocateIntArray(int num){
    int * ptr = (int *) malloc(num * sizeof(int));
    return ptr;
}

double findAverage(int * array, int num){
    int i;
    double average = 0.0;
    for(i=0;i<num;i++){
        average += array[i];
    }
    average = average / num;
    return average;
}
```



我对```scanf("%d",array+i);```中的array+i，有疑惑。



尝试在紧随这句之后，输出刚刚输入的值，则需要```printf("%d",*(array+i));```。



如果```printf("%d",array+i);```，则会出现错误提示：

**/user-input:19:21:** **warning:** **format specifies type 'int' but the argument has type 'int \*'**        printf("%d",array+i);



所以，```scanf("%d",array+i);```中的array+i，正合了```scanf("%d", array)```，array前可以略去&，因为array自带pointer属性。（Unit 4.1的3.1内容。）



## 3.3 Activity: dynamically allocate memory for strings

You are working  on programming a toaster (again!). The user of the toaster has the  option to have their bread toasted "light" or "dark", and you are  working on implementations in different languages of this particular  setting. For example, in the German model, the settings would be stored  as "hell" and "dunkel" instead. In order to be as efficient as possible  with the use of the limited memory on the computer chip in the toaster  you need to write a function "allocateString()" that allocates memory  for strings (and you will then use this function to allocate just enough memory to store the settings on a particular model).

This function "allocateString()" takes as argument  an integer (of type int), representing the number of characters to  allocate space for in memory. The function returns a pointer (of type  char *), containing the address of the allocated memory. The function  should use memory allocation to reserve the correct amount of space in  memory. In order to receive credit for your solution you need to use  sizeof (char) in this line, even if sizeof (char) returns 1.

In your main() function you should call the function allocateString() twice: once for the label containing the "light"  setting and once for the "dark" setting. You are provided with some code already that explains precisely what you need to do. Please do not  change the code that has been given to you. Please only change those  lines that say "// add a line of code...".

**Examples**

**Input:**

```
4 6
hell
dunkel
```

**Output: **

```
Local settings: hell - dunkel
```


**Provided code**

```c
#include <stdio.h>
// Be sure to include any other library you may need...

// Write your allocateString() prototype here

int main(void) {
    int lengthLight, lengthDark;
    char *strLight, *strDark;
    
    scanf("%d %d", &lengthLight, &lengthDark); 
    // Write a line of code here that calls the function allocateString(). 
    
    /* The goal is to reserve space for the light setting label, therefore you 
       need to pass the number lengthLight to the function allocateString()
       Store the return value of this function call in the variable strLight. */
     
    // Write a line of code here that calls the function allocateString().
    
    /* This time the goal is to reserve space in memory for the dark setting label.
       Store the return value of the function call in the variable strDark. */
   
    scanf("%s", strLight);
    scanf("%s", strDark);
    printf("Local settings: %s - %s\n", strLight, strDark);
    // Write a line of code here to free the memory allocated for strLight
    
    // Write a line of code here to free the memory allocated for strDark
    
	
    return 0;
}

char * allocateString(int numChars){
    // declare your variable(s) here
    
    // Write a line of code here that performs the memory allocation.
    /* You should allocate space in memory for the number of characters specified 
       via the input parameter to the function and the null terminator and store the 
       address of the allocated memory in a pointer named ptr. In order to receive credit 
       for your solution you need to use sizeof(char) in this line, even if sizeof(char) 
       returns 1. */
    
    return ptr;
}
```


**我的程序：**

```c
#include <stdio.h>
// Be sure to include any other library you may need...
char * allocateString(int);
// Write your allocateString() prototype here

int main(void) {
    int lengthLight, lengthDark;
    char *strLight, *strDark;
    
    scanf("%d %d", &lengthLight, &lengthDark); 
    // Write a line of code here that calls the function allocateString(). 
    strLight = allocateString(lengthLight);
    /* The goal is to reserve space for the light setting label, therefore you 
       need to pass the number lengthLight to the function allocateString()
       Store the return value of this function call in the variable strLight. */
     
    // Write a line of code here that calls the function allocateString().
    strDark = allocateString(lengthDark);
    /* This time the goal is to reserve space in memory for the dark setting label.
       Store the return value of the function call in the variable strDark. */
   
    scanf("%s", strLight);
    scanf("%s", strDark);
    printf("Local settings: %s - %s\n", strLight, strDark);
    // Write a line of code here to free the memory allocated for strLight
    free(strLight);
    // Write a line of code here to free the memory allocated for strDark
    free(strDark);
	
    return 0;
}

char * allocateString(int numChars){
    // declare your variable(s) here
    char * ptr = (char *) malloc(numChars * sizeof(char));
    // Write a line of code here that performs the memory allocation.
    /* You should allocate space in memory for the number of characters specified 
       via the input parameter to the function and the null terminator and store the 
       address of the allocated memory in a pointer named ptr. In order to receive credit 
       for your solution you need to use sizeof(char) in this line, even if sizeof(char) 
       returns 1. */
    
    return ptr;
}
```



**注意：**

```    scanf("%s", strLight);```
``` scanf("%s", strDark);```

中的strLight和strDark，不需要&。