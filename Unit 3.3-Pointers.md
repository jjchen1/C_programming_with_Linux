# 2 Defining pointers and dereferencing pointers

## 2.1 Get and print the address of a variable using pointers

### 2.1.2 分析程序

```c
#include <stdio.h>
int main(){
    //! showMemory(start=65520)
    int a = 42;
    double d = 58.394;
    char c = 'r';
    int * addressOfA = &a;
    printf("address of a: %p\n", addressOfA);
    double * addressOfD = &d;
    printf("address of d: %p\n", addressOfD);
    char * addressOfC = &c;
    printf("address of c: %p\n", addressOfC);
    return 0;
}
```



先出现a、b、c：

![image-20200326234718432](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326234718432.png)

下列语句，用于得到变量的地址：

```c
int * addressOfA = &a;
double * addressOfD = &d;
char * addressOfC = &c;
```



printf("%p", addressOfD);用于打印地址，**p意味着pointer**。



得到各个变量的address

![image-20200326235031662](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326235031662.png)



程序打印结果为：

```
address of a: fffc                                                              
address of d: fff4                                                              
address of c: fff3 
```



### 2.1.2 字节大小

上面程序得到的address，都是4 bytes（字节）大小，这对32 bits系统，是正确的。

如果是64 bits系统，则address是8 bytes（字节）。

因为**1 byte equals 8 bits**。



### 2.1.3 pointer

我们学会了如何建立address、得到从变量得到address的值、打印address。

上述变量addressOfA、addressOfD、addressOfC，被称为pointers。因为它们指向另一个变量（分别是a、d、c）



## 2.2 Dereference a pointer: get the value stored at a specific address

```c
#include <stdio.h>
int main(){
    //! showMemory(start=65520)
    double a = 42.98;
    double * addressOfA = &a;
    printf("At the address %p there is the value %.2lf\n",addressOfA,* addressOfA);
    char c = 'm';
    char * addressOfC = &c;
    char d = * addressOfC;
    * addressOfA = 32;
    * addressOfA = * addressOfA + 1;
    printf("At the address %p there is the value %.2lf\n",addressOfA,* addressOfA);
    return 0;
}
```

1. double * addressOfA = &a，定义一个变量的pointer，赋值为42.98；

![image-20200327123214841](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200327123214841.png)

2. 打印addressOfA和* addressOfA

```
At the address fff8 there is the value 42.98 
```



3. addressOfA = 32;给pointer对应的原变量赋值为32；

![image-20200327123338666](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200327123338666.png)

4. a最后赋值为33；

![image-20200327123403576](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200327123403576.png)

5. 打印

```
At the address fff8 there is the value 42.98                                    
At the address fff8 there is the value 33.00
```



## 2.3 Activity: use pointers to create elixir

You are developing an elixir that supposedly makes a person younger. You just need to get the software working correctly  before starting to market your product. Your program keeps track of a  person's age, but in order to be more secretive you work with a pointer  rather than the variable that stores the age directly. 

You are provided with a main function -- please  complete it. Do not change any of the lines of code that have already  been completed. Please only change the lines that are currently  comments.

### Provided code

```c
#include <stdio.h>

int main(void) {

    int age;

    // add a line here that declares an integer pointer named "ageptr"

    scanf("%d", &age);

    // add a line here that stores the address of age in ageptr  

    printf("The secret address is... ");

    // add a line here that prints out the address stored in ageptr  

    printf("Now take three drops of the magic elixir. \n");

    // add a line that uses only ageptr to lower the age by 5 years

    printf("Did the elixir work? You are %d years old!", age);

    return 0;

}
```

### Example

#### Input:

```
45
```

#### Output

```
The secret address is...fffc                                                    
Now take three drops of the magic elixir.                                       
Did the elixir work? You are 40 years old!
```



我的程序：

```c
#include <stdio.h>

int main(void) {

    int age;
    
    int * ageptr;// add a line here that declares an integer pointer named "ageptr"

    scanf("%d", &age);

    ageptr = &age; // add a line here that stores the address of age in ageptr 

    printf("The secret address is... ");

    printf("%p\n", ageptr);// add a line here that prints out the address stored in ageptr  

    printf("Now take three drops of the magic elixir. \n");

    * ageptr -= 5;// add a line that uses only ageptr to lower the age by 5 years

    printf("Did the elixir work? You are %d years old!", age);

    return 0;

}
```



# 3 Using pointers with functions

## 3.1 Swap two integer variable values using functions and pointers

1. main中的a，b值没改变。因此，需要pointer。

```c
#include <stdio.h>
void swap(int,int);
int main() {
     //! showMemory(start=65520)
     int a = 9;
     int b = 1;
     swap(a,b);
     printf("%d %d\n",a,b);
    return 0;
}
void swap(int a, int b){
    int tmp = a;
    a = b;
    b = tmp;
}
```



2. 将a、b的地址，用swap()函数交换，则可以实现a和b值的交换。

```c
#include <stdio.h>
void swap(int *,int *);
int main() {
     //! showMemory(start=65520)
     int a = 9;
     int b = 1;
     swap(&a,&b);
     printf("%d %d\n",a,b);
    return 0;
}
void swap(int * a, int * b){
    int tmp = * a;
    * a = * b;
    * b = tmp;
}
```



注意，此时swap()中的parameter，不同于main中的a。换成变量名addressOfa、addressOfb，更直观：

```c
#include <stdio.h>
void swap(int *,int *);
int main() {
     //! showMemory(start=65520)
     int a = 9;
     int b = 1;
     swap(&a,&b);
     printf("%d %d\n",a,b);
    return 0;
}
void swap(int * addressOfa, int * addressOfb){
    int tmp = * addressOfa;
    * addressOfa = * addressOfb;
    * addressOfb = tmp;
}
```



## 3.2 Modify an integer variable value using a function with pointers

1. main中和addThree()函数中的a值，并不相同。所以需要pointer。

```c
#include <stdio.h>
void addThree(int);
int main() {
    //! showMemory(start=65520)
    int a = 5;
    addThree(a);
    printf("inside main, value of a: %d\n",a);
    return 0;
}
void addThree(int a){
    a = a + 3;
    printf("inside addThree, value of a: %d\n",a);
}
```



输出：

```
inside addThree, value of a: 8                                                  
inside main, value of a: 5 
```



2. 将addThree中的参数改为pointer，则：

```c
#include <stdio.h>
void addThree(int *);
int main() {
    //! showMemory(start=65520)
    int a = 5;
    addThree(&a);
    printf("inside main, value of a: %d\n",a);
    return 0;
}
void addThree(int * a){
    *a = *a + 3;
    printf("inside addThree, value of a: %d\n",*a);
}
```



输出：

```
inside addThree, value of a: 8                                                  
inside main, value of a: 8 
```



注意，此时addThree()中的parameter，不同于main中的a。换成变量名addressOfa，更直观：

2. 

```c
#include <stdio.h>
void addThree(int *);
int main() {
    //! showMemory(start=65520)
    int a = 5;
    addThree(&a);
    printf("inside main, value of a: %d\n",a);
    return 0;
}
void addThree(int * addressOfa){
    * addressOfa = * addressOfa + 3;
    printf("inside addThree, value of a: %d\n",* addressOfa);
}
```

## 3.3 Activity: use pointers to improve elixir

You are continuing to work on your elixir of youth,  and it turns out that, before purchasing the elixir, customers would  like to know how young they will become after drinking the elixir!

The way your elixir works is that anyone who is at  least 21 years old becomes ten years younger. However, the elixir does  not work on anyone twenty years old or younger - when these people try  the elixir, they actually double in age!

You have already created a main function, shown  below. All you need to do now is write a function which accepts the  integer pointer "ageAddr" as an argument and modifies the integer this  pointer points to according to the rules of your elixir. Since you are  using pointers to change the value of the variable age, your function  should have a void return type. 

Be sure not to modify the code that has been given to you, other than to add the following:

- Your function definition.
- The appropriate function call where indicated in the main function.
- Your function prototype where indicated in the provided code.

```c
#include <stdio.h>

//Write your function prototype here

int main(void){
	int age;
	int *ageAddr = &age;
	scanf("%d", ageAddr);
	printf("Your current age is %d.\n", age);

	//Write your function call here

	printf("Your new age will be %d!\n", age);
	return 0;
}


//Write your function here
```

 

### Example

#### Input:

```
55
```

#### Output:

```
Your current age is 55.
Your new age will be 45!
```

#### Input:

```
19
```

#### Output:

```
Your current age is 19.
Your new age will be 38!
```



我的程序：

```c
#include <stdio.h>

void elixir(int *);//Write your function prototype here

int main(void){
	int age;
	int *ageAddr = &age;
	scanf("%d", ageAddr);
	printf("Your current age is %d.\n", age);

	elixir(ageAddr);//Write your function call here

	printf("Your new age will be %d!\n", age);
	return 0;
}

//Write your function here
void elixir(int * ageAddr){
    if (* ageAddr >= 21){
        * ageAddr -= 10;
    } else {
        * ageAddr *= 2;
    }
}
```





# 4 Performing simple pointer arithmetic

## 4.1 Introduction to pointer arithmetic: arrays, addresses and pointers

1. 注意，写入array时，以前就不加&，此处也是直接arr；通过pointer，改变了arr[0]的值

```c
#include <stdio.h>
int main() {
    //! showMemory(start=65520)
    int arr[3] = {15, 16, 17};
    printf("%p\n",arr);
    int * ptr = arr;
    * ptr = 2;
    return 0;
}
```



输出：

```
fff4                                                                            
```

![image-20200327140958146](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200327140958146.png)

2. (ptr+1)，意味着给地址增加了4个字节（bytes），这是array的1个element的大小。

注意到 pointer语句“int * ptr = arr;”，类型是int *；因为int，我们知道1个int的大小，是4个字节（bytes）。

总之，fff4增加了4，得到fffa，这对应着arr中的第2个元素。

于是，其值变为3。

```c
#include <stdio.h>
int main() {
    //! showMemory(start=65520)
    int arr[3] = {15, 16, 17};
    printf("%p\n",arr);
    int * ptr = arr;
    * ptr = 2;
    * (ptr + 1) = 3;
    return 0;
}
```

![image-20200327142301445](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200327142301445.png)

3. 改变arr的第3个元素

```c
#include <stdio.h>
int main() {
    //! showMemory(start=65520)
    int arr[3] = {15, 16, 17};
    printf("%p\n",arr);
    int * ptr = arr;
    * ptr = 2; // * arr   0R  arr[0]
    * (ptr + 1) = 3; // * (arr + 1)   OR  arr[1]
    * (ptr + 2) = 5;// * (arr + 2)   OR arr[2]
    return 0;
}
```

![image-20200327142503743](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200327142503743.png)



4. 注意，一定要加括号，下列格式，是无意义的：

```c
    * ptr + 1 = 3;
```



只会报错：

```
/user-input:10:15: error: expression is not assignable
    * ptr + 1 = 3;
    ~~~~~~~~~ ^
```



## 4.2 Activity: pointer arithmetic

题目：

![image-20200327145224485](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200327145224485.png)



做不出来，写成程序，得到答案：

```c
#include <stdio.h>

int main(void){
	int array[] = {4, 6, 12, -5, -7, 3, 1, 0, -10};
	int *ptr1, *ptr2;
	ptr1 = array+2;
	printf("array = %p\n", array);
	printf("array+2 = %p\n", array+2);
	printf("ptr1 = %p\n", ptr1);
	
	ptr2 = &ptr1[5];
	printf("ptr1[5] = %d, &ptr1[5] = %p\n", ptr1[5], &ptr1[5]);
	
	
	printf("(ptr1+1) = %p, *(ptr1+1) = %d\n", (ptr1+1), *(ptr1+1));
	printf("(ptr2-3) = %p, *(ptr2-3) = %d", (ptr2-3), *(ptr2-3));
	return 0;
}
```



输出：

```
array = ffdc                                                                    
array+2 = ffe4                                                                  
ptr1 = ffe4                                                                     
ptr1[5] = 0, &ptr1[5] = fff8                                                    
(ptr1+1) = ffe8, *(ptr1+1) = -5                                                 
(ptr2-3) = ffec, *(ptr2-3) = -7
```



分析过程：

![image-20200327151207769](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200327151207769.png)

# 5 Passing arrays to functions

## 5.1 Pass an array to a function



## 5.2 Activity: arrays and functions

