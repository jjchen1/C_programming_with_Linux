# Printing and computing with integers

## 2.1 Use format specifier %d to print integer value

```c
#include <stdio.h>
int main(void){
    printf("If I have %d bills worth %d dollars each then I have %d dollars.",3,5,3*5);
    return 0;
}
```



## 2.2 Perform simple integer arithmetic (+, -, *, ())

```c
#include <stdio.h>
int main() {
    printf("3+2 equals %d and 3-2 equals %d and 3*2 equals %d\n", 3+2, 3-2, 3*2);
    printf("3+2*3 equals %d and (3+2)*3 equals %d\n", 3+2*3, (3+2)*3);
    printf("2*8-2*7-4 equals %d\n", 2*8-2*7-4);
    printf("2*(8-2*(7-4)) equals %d\n", 2*(8-2*(7-4)));
    printf("2*(8-2*7)-4 equals %d\n", 2*(8-2*7)-4);
    return 0;
}
```



# 2.3 Activity: perform simple arithmetic in C

You work for the IBP (International Bureau of  Procrastination). You've been asked how much time is left until the  official day of procrastination (March 25th).

Given that you've been asked on March 23rd, please  write a C-program which performs arithmetic in order to produce the  following output:

```
Dear Procrastinator,
You still have to wait for X days (Y minutes or Z seconds) before you can procrastinate!
```

Here, X is the remaining number of days (25-23), Y  is the number of minutes (60 * 24 * X) and Z is the number of seconds  (60 * Y). The sentence has to be exactly the one displayed above,  replacing X, Y and Z with the computed values. The format has to be  followed precisely.

*Warning:* You cannot simply perform these  calculations yourself and print the values - your program must calculate them and print them using the %d format specifier.



答案：

```c
#include <stdio.h>

int main(void){
    printf("Dear Procrastinator,\n");
    printf("You still have to wait for %d days (%d minutes or %d seconds) before you can procrastinate!",  (25-23), (60 * 24 * (25-23)),  (60 * (60 * 24 * (25-23))));
    return 0;
}
```



# 3 Using variables

## 3.1 Store integers in variables

```c
#include <stdio.h>
int main(void) {
    //Create a variable to store an integer value
    int age;
    //Assigne a value to that variable
    age = 47;
    printf("I am %d years old.\n", age);
    printf("In %d years, I will be %d years old.\n", 8, age+8);
    printf("%d years ago, I was %d years old.\n", 11, age-11);
    return 0;
}
```



## 3.2 Change the value of a variable

```c
#include <stdio.h>
int main() {
    int balance;//creating a variable containing integer values
    balance = 50;//assigning the value 50 into the balance variable
    printf("I have %d dollars in my account\n",balance);
    //expense of 40 dollars
    balance = balance - 40;
    printf("I have %d dollars in my account\n",balance);
    //add 20 dollars in my account
    balance = balance + 20;
    printf("I have %d dollars in my account\n",balance);
    //expense of 30 dollars
    balance = balance - 30;
    printf("I have %d dollar in my account\n",balance);
    return 0;
}
```



## 3.3 Review: Declare and initialize integer variables

```c
#include <stdio.h>
int main(void) {
   int variable = 2; //variable declaration and initialization all in one step

   return 0;
}
```



# 4 Declaring and naming variables

## 4.1 Declare and initialize variables in 1-step

```c
#include <stdio.h>
int main() {
    //DECLARATION and DEFINITION
    int balance = 50;
    //USE
    printf("I have %d dollars in my account\n", balance);
    return 0;
}
```





## 4.2 Name your variables: do's and don'ts

```c
#include <stdio.h>
int main(void) {
    /* Variable names can use:  
    lowercase and uppercase letters (characters) and digits
    do not use special characters like @ # & " ...
    do not use accented characters like é è à ...
    do not start with a digit
    start only with a letter
    spaces are forbidden
     _ may be used instead of a space in the name of the variable
    YouCanUseUppercaseLettersBetweenWordsInsteadOfSpaces   */

    int validBalance;
    validBalance = 50;
    printf("I have %d dollars in my bank account.\n", validBalance);
    return 0;
}
```



## 4.3 Activity: declare and name variables

### 第1题

![image-20200323143520037](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200323143520037.png)

变量名的开头必须是字母或下划线（下划线也可以！），不能是数字。

实际编程中最常用的是以字母开头，而以下划线开头的变量名是系统专用的。



正确答案：

![image-20200323144506584](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200323144506584.png)



### 第3题

![image-20200323143556702](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200323143556702.png)

正确答案：

![image-20200323144542722](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200323144542722.png)



# 5 Repeating instructions with variables

## 5.1 Use variables in loops

```c
#include <stdio.h>
int main(void) {
    int i;
    int numberOfHazelnuts = 0;
    int distanceTraveled = 0;
    for(i = 0; i < 9 ; i++) {
        printf("At %d miles I have %d hazelnuts.\n", distanceTraveled, numberOfHazelnuts);
        distanceTraveled = distanceTraveled + 1;
        numberOfHazelnuts = numberOfHazelnuts + 3;
    }
    return 0;
}
```

## 5.2 Activity: print the x8 multiplication table

Your friend is having a lot of difficulties with  multiplication tables. He's having the most trouble with the multiples  of 8 table, and asks you to send him the multiples of 8 table so that he can learn it more easily. To do this, you decide to write a program  that prints the multiples of 8 table. Because you will use your code  again in the future to print other multiplcation tables, you decide to  use a loop and **only one print statement**.

Your program must use the following format to print the multiples of 8 table (be careful with spaces):

```
0x8 = 0
1x8 = 8
...
10x8 = 80
```

*Warning:* Your program will not be reusable  in the near future if you don't use a loop. You must use a loop to print the multiplication table.



答案：

```c
#include <stdio.h>
int main(void){
    int i;
    for (i=0; i<11; i++){
        printf("%dx8 = %d\n", i, i*8);
    }
    return 0;
}
```



# 6 Reading user input

## 6.1 Read integer user input using scanf()

```c
#include <stdio.h>
int main() {
    int age;//DECLARE
    printf("Whare is your age ?\n");
    scanf("%d",&age);
    printf("You are %d years old\n", age);//USE
    return 0;
}
```



## 6.2 Read multiple integers using one scanf() statement

输入多个变量，默认可用①回车，②空格，隔开。

如果用逗号隔开，那么只能读取第1个变量。

```c
#include <stdio.h>
int main(void) {
    int first, second, third;
    printf("Please enter three integers: ");
    scanf("%d%d%d", &first, &second, &third);
    printf("You entered: %d for first, %d for second, %d for third.\n", first, second, third);
    
    return 0;
}
```



但如果制定分隔符了，那么逗号也可以：

```c
#include <stdio.h>
int main(void) {
    int first, second, third;
    printf("Please enter three integers, separated by commas: ");
    scanf("%d,%d,%d", &first, &second, &third);
    printf("You entered: %d for first, %d for second, %d for third.\n", first, second, third);
    
    return 0;
}
```



## 6.3 Activity: read an integer and print table

n this activity, you want to improve your existing  multiplication program (that prints the 8 times table). Your program  should read an integer from the user (not you) and print the  multiplication table for the number that they enter.

### Examples

#### Input:

```
8
```

#### Output:

```
0x8 = 0
1x8 = 8
...
10x8 = 80
```

#### Input:

```
5
```

#### Output:

```
0x5 = 0
1x5 = 5
...
10x5 = 50
```



我的程序：

```c
#include <stdio.h>
int main(void){
    int i, number;
    scanf("%d", &number);
    for (i=0; i<11; i++){
        printf("%dx%d = %d\n", i, number, i*number);
    }
    return 0;
}
```



# 7 Reading user input inside a loop

## 7.1 Use scanf() inside a loop to read multiple user inputs

```c
#include <stdio.h>
int main() {
    int howMany = 0;
    int sum = 0;
    int numberRead = 0;
    printf("How many items do you want to add?\n");
    scanf("%d",&howMany);
    for(int i = 0; i < howMany; i++){
        scanf("%d",&numberRead);
        printf("I have read %d from the input terminal\n",numberRead);
        sum = sum + numberRead;
        printf("sum equals %d\n",sum);
    }
  return 0;
}
```







## 7.2 Activity: read and process multiple integers via a loop

Here is your final activity of this unit. Use it to  apply everything you have learned! David is fighting Goliath (again...)  and it turns out that Goliath is much bigger than David thought.  Fortunately David is not short of resources and he plans to send robots  to fight the giant. But before launching the assault, David must  evaluate the performance of these robots to ensure success. This is  where you come in. You are given some data on David's robots and need to compute and output a corresponding power score.

Here is how: You should write a program that takes  several lines of input from a user (see the below example). The first  line of the input indicates the number of robots to be deployed. Each  subsequent line shows the height, the weight, the power of the engines  and a resistance rating (1,2, or 3) of each of of these robots. Your  program should use this information to calculate the total power of  these robots. The power of all robots is the sum of the power of each  robot, where the power of an individual robot is calculated via:

```
(enginePower + resistance) * (weight - height)
```

### Example

#### Input:

```
2
50 60 2 1
43 62 5 2
```

#### Output:

```
163
```

Here the output in this example is the calculation

(2 + 1) * (60-50) + (5 + 2) * (62-43)

You must use a loop to read each of the lines!

*Warning:* Your program must allow David to evaluate any army he gives as an input, not just the one given as an example.



我的程序：

```c
#include <stdio.h>
int main(void){
    int i;
    int howMany = 0;
    int height, weight, enginePower, resistance = 0;
    int sumPower = 0;
    scanf("%d", &howMany);
    for (i=0; i<howMany; i++){
        scanf("%d%d%d%d", &height, &weight, &enginePower, &resistance);
        sumPower = sumPower + (enginePower + resistance) * (weight - height);
    }
    printf("%d", sumPower);
    return 0;
}
```