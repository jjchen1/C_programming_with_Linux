# 2 Defining functions and passing values to functions

## 2.1 Write a function: the sum of 2 integers

```c
#include <stdio.h>
int sum(int x, int y){
    int compute;
    printf("Starting the computation!\n");
    compute = x+y;
    printf("Finished the computation successfully!\n");
    return compute;
}
int main(void) {
    int a,b;
    int result;
    printf("Please enter two numbers: ");
    scanf("%d%d", &a, &b);
    printf("You entered %d and %d.\n", a, b);
    result = sum(a, b);
    printf("Result of the sum = %d.\n", result);
    return 0;
}
```



## 2.2 Differentiate parameters and arguments of a function

```c
#include <stdio.h>
int sum(int x, int y){ //x, y: PARAMETERS
    int compute;
    printf("Starting the computation!\n");
    compute = x + y;
    printf("Finished the computation successfully!\n");
    return compute;
}
int main(void) {
    int a, b;
    int result;
    printf("Please enter two integers: ");
    scanf("%d%d", &a, &b);
    printf("You entered %d and %d.\n", a, b);
    result = sum(a, b);//a, b: ARGUMENTS
    printf("Result of the sum = %d.\n", result);
    return 0;
}
```



## 2.3 Differentiate the prototype and the definition of a function

sum函数的定义，要在main函数上方，否则无法识别。

如果就想把sum函数放下面，则在main函数前，先用一行prototype说明parameter的类型，再调用！

```c
#include <stdio.h>
int sum(int, int); //function PROTOTYPE
int main(void) {
    int a, b;
    int result;
    printf("Please enter two integers: ");
    scanf("%d%d", &a, &b);
    printf("You entered %d and %d.\n", a, b);
    result = sum(a, b); //copies of the VALUES of the ARGUMENTS a and b
    printf("Result of the sum = %d.\n", result);
    return 0;
}
// Function DEFINITION
int sum(int x, int y){ //values are copied into PARAMETERS x and y
    int compute;
    printf("Starting the computation!\n");
    compute = x + y;
    printf("Finished the computation successfully!\n");
    return compute;
}
```



# 3 Working with functions

## 3.1 Decompose a problem into multiple functions

```c
#include <stdio.h>
void printLine(int nCols, char pattern);
void printTriangle(int nLines, char pattern);
void printRectangle(int nLines, int nCols, char pattern);

int main(void)
{
   int nCols;
   int nLines;
 
   printf("How many columns would you like? ");
   scanf("%d", &nCols);
   printLine(nCols, 'X');
 
   printf("How many lines would you like? ");
   scanf("%d", &nLines);
   printTriangle(nLines, '*');
   printf("\n");
   printRectangle(nLines, nCols, '#');
}

void printLine(int nCols, char pattern)
{
   int i;
   for (i = 0; i < nCols; i++)
   {
      printf("%c", pattern);
   }
   printf("\n");
}
 
void printTriangle(int nLines, char pattern)
{
   int line, cols;
   for (line = 0; line < nLines; line++)
   {
      cols = line + 1;
      printLine(cols, pattern);
   }
}
 
void printRectangle(int nLines, int nCols, char pattern)
{
   int i;
   for (i = 0; i < nLines; i++){
      printLine(nCols, pattern);
   }
}
```



## 3.2 Correct basic compilation errors with functions

```c
#include <stdio.h>
int sum(int, int);
int main(void){
    int result;
    result = sum(10, 4);
    printf("The sum  is %d.\n", result);
    return 0;
}

int sum(int x, int y) {
    int compute;
    compute = x+y;
    return compute;
}
```



## 3.3 Activity: program a smart unit converter

Write a C-program that converts metric measurements  to imperial system values. Measurements are provided to your program in  meters, grams or degrees Celsius and must be converted to feet, pounds  and degrees Fahrenheit, respectively.

Here are the conversion rules to use:

1 meter = 3.2808 feet;

1 gram = 0.002205 pounds;

temperature in degrees Fahrenheit = 32 + 1.8 × temperature in degrees Celsius.

On the first input line you are given the number of  conversions to be made. Each of the following lines contains a value to  be converted as well as its unit: m, g or c (for meters, grams or  degrees Celsius). There will be a space between the number and the unit. You should print your output value for each input line immediately  after calculating it (ie, you do not have to wait until you have read  all inputs).

Display the converted values with 6 decimal places,  followed by a space and their unit: ft, lbs or f (for feet, pounds or  degrees Fahrenheit). Each conversion result should be printed on its own line, and you should store and display all decimal values as doubles.

You may use functions to complete this exercise, but that is not required. However, you will need to use a comparison  operation with characters, for example:

```
char letter = 'a';

if(letter == 'a') {...}
```

 

### Example

The following entry indicates that there are four  values to be converted. The first is 10 meters, which, when converted,  gives approximately 32.808 feet. The second is 1245.243 grams, or about  2.745761 pounds, the third is 37.2 degrees Celsius, or 98.96 degrees  Farenheit, and the fourth is 23 grams, or 0.050715 pounds.

#### Input

```
4
10 m
1245.243 g
37.2 c
23 g
```

 

#### Output

```
32.808000 ft
2.745761 lbs
98.960000 f
0.050715 lbs
```



我的程序：

```c
#include <stdio.h>
void convertM(double);
void convertG(double);
void convertC(double);

int main(void){
    int number, i;
    double digit;
    char sign[1];
    scanf("%d", &number);
    for (i=0; i<number; i++){
        scanf("%lf %c", &digit, &sign[0]);
        if (sign[0] == 'm') {
            convertM(digit);
        } else if (sign[0] == 'g') {
            convertG(digit);
        } else if (sign[0] == 'c') {
            convertC(digit);
        }
    }
    return 0;
}

void convertM(double X){
    printf("%.6lf ft\n", 3.2808*X);
}

void convertG(double X){
    printf("%.6lf lbs\n", 0.002205*X);
}

void convertC(double X){
    printf("%.6lf f\n", 32+1.8*X);
}
```

注意，如果第12行，写成scanf("%lf %s", &digit, sign);，那么digit无法读取数据。我也不知道为什么，只是自己调试出来正确的程序。



## 3.5 Activity: find the smallest integer

The goal of this problem is to find the smallest integer in a list of numbers.

To help you with this task, please write a function  called min() that finds and returns the smallest amongst two integers  (be sure to also write a prototype for this function). The function thus takes two integers as input and returns the smallest of the two. This  function will use an if statement with a condition that contains either  "less than" or "greater than".

Next, please use min() in your main function to work your way through an entire list of numbers in order to find its  minimum. The first number you read gives the number of elements in the  list of integers under consideration. You will then read the integer  values, using min() to keep only the smallest integer read at each step. In the end, please print out the smallest integer in the list.

### Example

#### Input

```
10
4 3 6 2 6 8 9 8 5 4
```

#### Output

```
2
```



我的程序：

```c
#include <stdio.h>
int min(int, int);

int main(void){
    int number, i;
    int list[100];
    int minNum;
    
    scanf("%d", &number);
    
    scanf("%d", &list[0]);
    minNum = list[0];
    
    for (i=1; i<number; i++){
        scanf("%d", &list[i]);
        minNum = min(list[i], minNum);
    }
    
    printf("%d", minNum);
    return 0;
}

int min(int X, int Y){
    if (X <= Y){
        return X;
    } else {
        return Y;
    }
}
```



# 4 Using recursion

## 4.1 Use recursion to make a function use itself: the factorial example

```c
#include <stdio.h>
// 5! = 1*2*3*4*5
// n! = 1*2*3*...*(n-1)*n
int main(void) {
    int n, facto, i;
    printf("Please enter a positive integer: ");
    scanf("%d",&n);
    facto = 1;
    for(i=1 ; i<=n ; i++){
        facto = i*facto;
    }
    if(n<0){
        printf("%d is negative! Aborting..\n", n);
    }else{
        printf("%d! = %d.\n", n , facto);
    }
    return 0;
}
```



## 4.2 Use recursion to make a function use itself: the recursive factorial example

```c
#include <stdio.h>
// 5! = 1*2*3*4*5
// n! = 1*2*3*...*(n-1)*n
// recursion : one function calls itself
int factorial(int);
int main(void) {
    int n, facto;
    printf("Please enter a positive integer: ");
    scanf("%d",&n);
    if(n<0){
        printf("%d is negative! Aborting..\n", n);
    }else{
        facto = factorial(n);
        printf("%d! = %d.\n", n , facto);
    }
    return 0;
}
int factorial(int n){
    int result;
    if(n==0){
        result=1;
    }else{
        result = n * factorial(n-1);
    }
    return result;
}
```



## 4.3 Use recursion to make a function use itself: the Fibonacci example

```c
// Fibonacci numbers: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, ...
int fibonacci(int);
#include <stdio.h>
int main(void) {
    //! showMemory(start=65520)
    int N, fib;
    printf("Which Fibonacci number would you like: ");
    scanf("%d", &N);
    if (N<=0) {
        printf("%d is not positive. Aborting!\n", N);
    } else {
        fib = fibonacci(N);
        printf("The %dth Fibonacci number is %d.\n", N, fib);
    }
	return 0;
}

int fibonacci(int n) {
    if (n==1) {
        return 0;
    } else if (n==2) {
        return 1;
    } else {
        return (fibonacci(n-1) + fibonacci(n-2));
    }
}
```



## 4.4 Activity: use recursion to compute the sum of digits

Please write a C-program that uses a recursive  function called "sumOfDigits()" to compute the sum of the digits of a  number. To do so, your main function should first read an integer number as input and then call sumOfDigits(), which should in turn call itself  until there are no digits left to sum, at which point the final sum  should display to the user.

Here is the main idea of how the recursion in sumOfDigits() should work:

sumOfDigits(6452) = 2 + sumOfDigits(645)

sumOfDigits(645) = 5 + sumOfDigits(64)

...

sumOfDigits(6) = 6

### Examples

#### Input

```
47253
```

#### Output

```
21
```

 

#### Input

```
643
```

#### Output

```
13
```



我的程序：

```c
#include <stdio.h>
int sumOfDigits(int);

int main(void){
    int n;
    scanf("%d", &n);
    printf("%d", sumOfDigits(n));
    return 0;
}

int sumOfDigits(int X){
    if (X/10 == 0){
        return X;
    } else {
        return (X%10 + sumOfDigits(X/10));
    }
}
```