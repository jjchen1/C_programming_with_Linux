[TOC]

# 1 Using characters

## 1.1 Declare, assign and print characters with the %c format specifier

```c
#include <stdio.h>
int main(void) {
    char letter;//DECLARE A CHARACTER VARIABLE
    letter = 'a';//DEFINE or INITIALIZE or ASSIGN a character value
    printf("The letter is %c",letter);
    return 0;
}
```



## 1.2 Activity: print characters

Write a C-program that displays the following:

```
Programming in C
```

using this printf statement:

```c
printf ("Programming %c%c %c\n", letter1, letter2, letter3);
```

*Warning:* do not use a scanf statement in this exercise!



**我的程序：**

```c
#include <stdio.h>
int main(void){
    char letter1, letter2, letter3;
    letter1 = 'i';
    letter2 = 'n';
    letter3 = 'C';
    printf ("Programming %c%c %c\n", letter1, letter2, letter3);
}
```



# 2 Read characters from the user input

## 2.1 Read characters from the user input

输入的字符，可以用默认的空格/回车隔开，也可以制定用空格/逗号隔开。

```c
#include <stdio.h>
int main(void) {
    char letter, letter2;
    printf("Please enter two letters: ");
    scanf("%c%c", &letter, &letter2);
    printf("I read the letters %c and %c.\n", letter, letter2);
  
    printf("Please enter two letters separated by a space: ");
    scanf("%c %c", &letter, &letter2);
    printf("I read the letters %c and %c.\n", letter, letter2);
  
    printf("Please enter two letters separated by a comma: ");
    scanf("%c,%c", &letter, &letter2);
    printf("I read the letters %c and %c.\n", letter, letter2);
    return 0;
}
```



## 2.2 Activity: read characters

Write a C-program that reads an input character  (using scanf) and displays the following pyramid pattern using the  character read: 

**Examples**

**Input**

```
#
```

**Output**

```
++++#++++
+++###+++
++#####++
+#######+
#########
```

**Input**

```
o
```

**Output**

```
++++o++++
+++ooo+++
++ooooo++
+ooooooo+
ooooooooo
```



**我的程序：**

```c
#include <stdio.h>
int main(void){
    char letter;
    scanf("%c", &letter);
    printf("++++%c++++\n", letter);
    printf("+++%c%c%c+++\n", letter, letter, letter);
    printf("++%c%c%c%c%c++\n", letter, letter, letter, letter, letter);
    printf("+%c%c%c%c%c%c%c+\n", letter, letter, letter, letter, letter, letter, letter);
    printf("%c%c%c%c%c%c%c%c%c\n", letter, letter, letter, letter, letter, letter, letter, letter, letter);
    return 0;
}
```



# 3 Using decimal

## 3.1 Declare, assign and print decimal numbers

小数位数，比实际的多，就补上0；比实际的少，就四舍五入。

```c
#include <stdio.h>
int main(void) {
    double height;
    height = 1.99;
    printf("I am %.1lf meters tall.",height);
    return 0;
}
```



## 3.2 Read decimal numbers from user input with scanf()

```c
#include <stdio.h>
int main(void) {
    double height;
    printf("How tall are you (in meters)? ");
    scanf("%lf", &height);
    printf("I am %.2lf meters tall.", height);
    return 0;
}
```



## 3.3 Read integers and doubles with scanf()

```c
#include <stdio.h>
int main(void) {
    int age;
    double height;
    printf("What is your age?");
    scanf("%d",&age);
    printf("What is your height?");
    scanf("%lf",&height);
    printf("You are %d years old and %.2lf meters tall.",age,height);
    return 0;
}
```



## 3.4 Read integers and doubles with one scanf() statement

```c
#include <stdio.h>
int main(void) {
    int age;
    double height;
    printf("What is your age and height (separate with spaces)?");
    scanf("%d %lf",&age,&height);
    printf("You are %d years old and %.2lf meters tall.",age,height);
    return 0;
}
```



## 3.5 Activity: read a decimal number

Petra, Rémi and their families went hiking in the  mountains together and realized that distances are measured in  different units in France and the United States. To help them convert  between units, please write a program that reads a decimal number  representing a distance in kilometers and that prints out the  corresponding distance in miles with 6 decimal places. 

You may use the fact that one kilometer equals 0.621371 miles. 

**Examples**

**Input:**

```
4.8
```

**Output: **

```
2.982581
```



**我的程序：**

```c
#include <stdio.h>
int main(void) {
    double mile;
    scanf("%lf", &mile);
    printf("%.6lf", mile*0.621371);
    return 0;
}
```



# 4 Divide in C

## 4.1 Divide in C

### 4.1.1 整数相除，截断小数，而不是四舍五入

5/2，得到2

5/3，得到1

```c
#include <stdio.h>
int main(void) {
    // integer division
    printf("5/2 equals %d\n", 5/2);
    return 0;
}
```



### 4.1.2 分子分母都是整数，输出就应该是整数格式%d

否则会warning，“printf("5/2 equals %lf\n", 5/2);”输出2.000000；



### 4.1.3 分子分母中，只要有一个小数，输出就应该是小数格式%lf，

否则会warning，“printf("5.0/2 equals %d\n", 5.0/2);”输出2.5；

（warning，不是error，还是会可以输出的）

```c
#include <stdio.h>
int main(void) {
    // integer division
    printf("5/2 equals %d\n", 5/2);
    // floating point division
    printf("5.0/2.0 equals %lf\n", 5.0/2.0);
    printf("5/2.0 equals %lf\n", 5/2.0);
    printf("5.0/2 equals %lf\n", 5.0/2);
    return 0;
}
```



## 4.3 Activity: divide numbers

When Rémi came to the US (to visit Petra to make  this MOOC) he brought his favorite cookie recipe! When trying to bake  the cookies he realized that ovens in the US show temperature in degrees Fahrenheit, but the cookie recipe called for a temperature in degrees  Celsius. We need your help!

Please write a C-program that reads a decimal number representing a temperature in degrees Celsius and prints out the  corresponding temperature in degrees Fahrenheit with 1 decimal place.  Here is the conversion formula:

Temperature (°F) = Temperature (°C) × 9.0 / 5.0 + 32.0

**Examples**

**Input:**

```
192
```

**Output: **

```
377.6
```

 

**Input:**

```
30.5
```

**Output: **

```
86.9 
```

*Warning*: You will be graded on your output, so do not include any print statements that prompt a user for input.



**我的程序：**

```c
#include <stdio.h>
int main(void) {
    double temp;
    scanf("%lf", &temp);
    printf("%.1lf", temp * 9.0/5.0 +32.0);
    return 0;
}
```



# 5 Find the remainder

## 5.1 Find the remainder in integer division

```c
#include <stdio.h>
int main(void) {
    // pay 166 dollars using 20-dollar bills, rest with 1-dollar bills
    int twenties = 166/20;
    int rest = 166%20;
    printf("I will pay %d dollars with 20-dollar bills.\n", twenties * 20);
    printf("I will then pay %d dollars with 1-dollar bills.\n", rest);
    return 0;
}
```



## 5.2 Activity: find the remainder in integer division

You have a number of loose matches that you would  like to put back into boxes. Write a program that calculates and  displays how many full boxes you will have and how many leftover matches you will have after filling all the boxes you can. Your program should  take as input the number of matches to be boxed up followed by the size  of a each box. Next it should print out the number of full boxes  followed by the number of remaining matches.

**Examples**

**Input:**

```
666
13
```

**Output: **

```
51
3
```



**我的程序：**

```c
#include <stdio.h>
int main(void) {
    int a, b;
    scanf("%d%d",&a, &b);
    printf("%d\n%d", a/b, a%b);
    return 0;
}
```



# 6 Converting integers to decimals

## 6.1 Convert integers to double

```c
#include <stdio.h>
int main(void) {
    int iOne;
    int iTwo;
    double dOne;
    printf("Please enter two integers: ");
    scanf("%d %d",&iOne, &iTwo);
    dOne = (double) iOne;
    printf("dOne/iTwo equals %lf\n",dOne/iTwo);
    return 0;
}
```



## 6.2 Activity: convert integers to doubles

You are helping a teacher average grades. You get  bored computing averages by hand, so you decide to write a computer  program to do the work for you.

Your program must first read an integer indicating  the number of grades to be averaged. Next, your program will read the  grades one by one, all of which are integers as well. Finally, your  program will calculate and print the average of the grades **to two decimal places**.

**Examples**

**Input:**

```
4
10
8
16
9
```

**Output: **

```
10.75
```

 *Warning*: You will be graded on your output, so do not include any print statements that prompt a user for input.



**我的程序：**

```c
#include <stdio.h>
int main(void){
    int number, grade, i;
    int sum=0;
    double dSum;
    scanf("%d", &number);
    for (i=0; i<number; i++){
        scanf("%d", &grade);
        sum = sum + grade;
    }
    dSum = (double)sum;
    printf("%.2lf", dSum/number);
    return 0;
}
```



# 7 Converting decimals to integers

## 7.1 Convert double to integers

double转int，是截断，而不是四舍五入。

```c
#include <stdio.h>
int main(void) {
    double dOne, dTwo;
    int iOne, iTwo;
    printf("Please enter two decimals: ");
    scanf("%lf %lf", &dOne, &dTwo);
    printf("I read dOne = %lf, dTwo = %lf.\n", dOne, dTwo);
    iOne = (int) dOne;
    iTwo = (int) dTwo;
    printf("iOne = %d, iTwo = %d.\n", iOne, iTwo);
    printf("%d / %d = %d.\n", iOne, iTwo, iOne/iTwo);
    return 0;
}
```



terminal运行结果：

```
Please enter two decimals: 5.0 2.0                                              
I read dOne = 5.000000, dTwo = 2.000000.                                        
iOne = 5, iTwo = 2.                                                             
5 / 2 = 2. 
```



## 7.2 Activity: convert doubles to integers

The population of a city has risen sharply over the  past few years, thanks to a high birth rate. However, this poses a  number of problems, including a housing shortage. The mayor has decided  to deal with the problem and would like to estimate the future growth of the population, and he has called you in to help!

Please write a C-program that first reads an integer representing the current population of the city, and that next reads a  decimal number for the projected population growth as a percentage  (either positive or negative). The program should then display the  expected population of the city in a year as a whole number. By  convention we will only consider "whole" people. So a population of 31.8 inhabitants will be considered as having 31 inhabitants. 

**Examples**

**Input:**

```
123
7.0
```

**Output: **

```
131
```



**我的程序：**

```c
#include <stdio.h>
int main(void){
    int pupulation;
    double percentage;
    scanf("%d%lf", &pupulation, &percentage);
    printf("%d", (int)(pupulation*(1+percentage/100.0)));
    return 0;
}
```



# 8 Practicing division

## 8.1 Activity: divide decimals

You just started learning a new language and decide  to buy a few books to practice. Thankfully you quickly find a book  seller who offers every book for the same low fixed price. You have a  certain amount of money and you would like to know how many books of the same price you can purchase.

Please write a C-program that starts by reading the  amount of money you have (which may be a double), then reads the price  per book (which again may be a double). The program should then display  an integer, namely the largest number of books that you can purchase  with the given amount of money.

**Examples**

**Input:**

```
48.0
3.50
```

**Output: **

```
13
```

**Input:**

```
27.0
5.0
```

**Output: **

```
5
```

*Warning:* You will be graded on your output, so do not include any print statements that prompt a user for input.



**我的程序：**

```c
#include <stdio.h>
int main(void){
    double moneyAll, moneyEach;
    scanf("%lf%lf", &moneyAll, &moneyEach);
    printf("%d", (int)(moneyAll/moneyEach));
    return 0;
}
```



## 8.2 Activity: divide decimals with round-off

You are building a new home and you have calculated  exactly how much cement you need for the foundation. Ideally you'd like  to purchase this exact amount of cement, but the store only sells cement in 120-pound bags. Each of these bags costs 45 dollars. Please write a  C-program that calculates the cost of the cement you will have to  purchase to build your foundation.

Your program should first read a decimal number  representing the amount of cement needed (in pounds) for the foundations of your new home. Your program should then display the total cost of  the cement bags you have to purchase to have enough cement to build your foundation. **To make your program simpler, you are guaranteed that the  amount of cement needed will NEVER be a multiple of 120.**（否则，就要难很多。）

**Examples**

**Input:**

```
295.8
```

**Output: **

135


In this example, you need 295.8  pounds of cement. Since the store only sells cement in increments of 120 pounds, you will need three bags (360 pounds) since 2 bags (240 pounds) is not enough and you cannot buy fractions of a bag. Since bags cost  $45 each, the total cost is 45 * 3, or 135 dollars.



**我的程序：**（无法应对weight是120的整数倍的情况）

```c
#include <stdio.h>
int main(void){
    double weight;
    int money;
    scanf("%lf", &weight);
    money = 45 * (int)(weight/120.0 + 1.5); 
    //(int)(a+0.5)实现四舍五入，(int)(a+1.5)实现四舍五入后+1
    printf("%d", money);
    return 0;
}
```

