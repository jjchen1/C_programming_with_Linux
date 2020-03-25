# 1 Using the if statement

## 1.1 Use an if statement with a static condition

0和0.0代表假，其余数字代表真

```c
#include <stdio.h>
int main(void) {
    // if it is true then do this
    // if it is not true, then do not do this
    //FALSE 0 0.0
    //TRUE all vallues that are non-zero (positive or negative)
    if(23){
        printf("Condition is true, I am executing this line.");
    }
    return 0;
}
```



```c
#include <stdio.h>
int main(void) {
    // if it is true then do this
    // if it is not true, then do not do this
    //FALSE 0 0.0
    //TRUE all vallues that are non-zero (positive or negative)
    if(0){
        printf("Condition is true, I am executing this line.");
    }
    return 0;
}
```



还可以用变量：

```c
#include <stdio.h>
int main(void) {
    // if it is true then do this
    // if it is not true, then do not do this
    //FALSE 0 0.0
    //TRUE all vallues that are non-zero (positive or negative)
    int weatherIsGood = 99; //the weather is good!
    if(weatherIsGood){
        printf("The weather is good!\n");
        printf("I can go outside! Yeah!\n");
    }
    return 0;
}
```



```c
#include <stdio.h>
int main(void) {
    // if it is true then do this
    // if it is not true, then do not do this
    //FALSE 0 0.0
    //TRUE all vallues that are non-zero (positive or negative)
    int weatherIsGood = 0;
    if(weatherIsGood){
        printf("Condition is true, I am executing this line.");
    }
    return 0;
}
```



## 1.2 Use if and else with a static condition

```c
#include <stdio.h>
int main(void) {
    // if it is true, do this
    // if it is false, do not do this
    //FALSE : 0  0.0  
    //TRUE : all the other values (positive or even negative)
    int weatherIsGood = 0; // It's cloudy!!
    if(weatherIsGood){
        printf("The weather is good!\n");
        printf("That's great, I can go outside!\n");
    }else{
        printf("The weather is bad!\n");
        printf("Too bad, I have to stay home!\n");
    }
    return 0;
}
```



## 1.3 Use an if statement with a dynamic condition

```c
#include <stdio.h>
int main(void) {
    // + - * / % : arithmetic operators
    // < > <= >= != == : comparison operators
    int a = 5;
    int b = 2;
    int result;
    printf("Check: Is a == b?\n");
    result = a==b;//加上括号，也许没那么奇怪了，但括号不是必须的：result = (a==b)
    printf("Result is %d.\n", result);
    if (result) {
        printf("TRUE!\n");
    } else {
        printf("FALSE!\n");
    }
    return 0;
}
```



## 1.4 Activity: if statements: carpooling

You are planning a car trip so you post on a carpooling website in order to share the cost of the trip.

If you have 0 passengers the carpool site does not  charge anything and you alone pay the full cost of the trip. If you have 1 or more passengers the carpool site adds a $1 fee to the cost of the  trip and evenly divides the total cost ($1 fee + gas) among the  passengers and you. You want to write a program that calculates the cost you have to pay. The program should read the number of passengers (an  integer) and the cost of gas for the trip (a decimal number). The  program should then print the cost that you have to pay (a decimal  number) with 2 digits after the decimal point. 

### Examples

#### Input

```
0 23.9
```

#### Output

```
23.90
```

 

#### Input

```
2 45.5
```

#### Output

```
15.50
```

 

#### Input

```
3 34.8
```

#### Output

```
8.95
```

*Warning:* You will be graded on your output, so do not include any print statements that prompt a user for input.



我的程序：

```c
#include <stdio.h>
int main(void){
    int number;
    double money, gas;
    scanf("%d%lf", &number, &gas);
    if (number == 0){
        money = gas;
    } else {
        money = (1+gas)/(number+1);
    }
    printf("%.2lf", money);
    return 0;
}
```



## 1.5 Activity: if statements: youth hostel

The hostel in which you plan to spend the night  tonight offers very interesting rates, as long as you do not arrive too  late. Housekeeping finishes preparing rooms by noon, and the sooner  guests arrive after noon, the less they have to pay. You are trying to  build a C program that calculates your price to pay based on your  arrival time.

Your program will read an integer (between 0 and 12) indicating the number of hours past noon of your arrival. For example, 0 indicates a noon arrival, 1 a 1pm arrival, 12 a midnight arrival, etc.  The base price is 10 dollars, and 5 dollars are added for every hour  after noon. Thankfully the total is capped at 53 dollars, so you'll  never have to pay more than that. Your program should print the price  (an integer) you have to pay, given the input arrival time.

### Example 1

#### Input

```
7
```

#### Output

```
45
```

### Example 2

#### Input

```
10
```

#### Output

```
53
```

*Warning*: You will be graded on your output, so do not include any print statements that prompt a user for input.



我的程序：

```c
#include <stdio.h>
int main(void){
    int number, money;
    scanf("%d", &number);
    money = 10 + 5*number;
    if (money < 53){
        printf("%d",money);
    } else {
        printf("%d", 53);
    }
    return 0;
}
```



# 2 Comparing decimal numbers

## 2.1 Branch program flow using floating point numbers

如果double类型的数字，只有小数位数超出double精度的部分有差别时，那么double会认为2者相等。

```c
    double a = 5.0000000000000000001;
    double b = 5.0000000000000000000;
    /* a==b, TRUE
    a > b, FALSE
    a < b, FALSE
    */
```



如果在double精度内，则没有问题：

```c
#include <stdio.h>
int main(void) {
    // + - * / % : arithmetic operations
    // <  >  <=  >=  !=  ==  :  comparison operations
    double a = 5.000000000001;
    double b = 5.000000000000;
    int result;
    printf("Check: Is a == b ?\n");
    result = a == b;
    printf("result is %d\n", result);
    if(result){
        printf("TRUE\n");
    }else{
        printf("FALSE\n");
    }
    return 0;
}
```



## 2.2 Activity: if statements: bridge tax

You arrive in front of a bridge that you must cross  to reach a village before dark. Crossing the bridge is not free - the  bridgekeeper asks you to roll two dice to determine the cost. You decide to write a program to verify that he is charging the right price.

Your program should read two integers, between 1 and 6, representing the values of each die. If the sum is greater than or  equal to 10, then you must pay a special fee (36 coins). Otherwise, you  pay twice the sum of the values of the two dice. Your program must then  display the text "Special tax" or "Regular tax" followed by the amount  you have to pay on the next line.

### Example

#### Input

```
5
6
```

#### Output

```
Special tax
36
```

 

#### Input

```
4
3
```

#### Output

```
Regular tax
14
```

*Warning*: You will be graded on your output, so do not include any print statements that prompt a user for input.



我的程序：

```c
#include <stdio.h>
int main(void){
    int num1, num2;
    scanf("%d%d", &num1, &num2);
    if (num1+num2 >= 10){
        printf("Special tax\n%d", 36);
    } else {
        printf("Regular tax\n%d", 2*(num1+num2));
    }
    return 0;
}
```



## 2.4 Activity: if statements, Tug of War

You decide to bet on the final match of the Tug of War National Championship. 

Prior to the match the names and weights of the  players are presented, alternating by team (team 1 player 1, team 2  player 1, team 1 player 2, and so on). There is the same number of  players on each side. You record the player weights as they are  presented and calculate a total weight for each time to inform your bet. You write a C program to assist with this.

Your program should first read an integer indicating the number of members per team. Then, the program should read the  player weights (integers representing kilograms) alternating by team. 

After calculating the total weight of each team, the program should display the text "Team X has an advantage" (replacing X  with 1 or 2 depending on which team has a greater total weight).

You will then display the text "Total weight for  team 1:" followed by the weight of team 1, then "Total weight for team  2:" followed by the weight of team 2 (see example below).

You are guaranteed that the two teams will not have the same total weight.

### Example

Each team is composed of four players. Those of the  first weigh 110, 113, 112, and 117kg, while those of the second weigh  106, 102, 121, and 111kg. Team 1 weighs a total of 452kg whereas team 2  weighs a total of 440kg, giving team 1 an advantage.

#### Input

```
4
110
106
113
102
112
121
117
111
```

#### Output

```
Team 1 has an advantage
Total weight for team 1: 452
Total weight for team 2: 440
```

我的程序：

```c
#include <stdio.h>
int main(void){
    int num, i, score, sum1, sum2;
    sum1 = 0;
    sum2 = 0;
    scanf("%d", &num);
    for (i=0; i<2*num; i++){
        scanf("%d", &score);
        if (i%2 == 0){
            sum1 = sum1 + score;
        } else {
            sum2 = sum2 + score;
        }
    }
    
    if (sum1 > sum2){
        printf("Team 1 has an advantage\n");
    } else {
        printf("Team 2 has an advantage\n");
    }
    
    printf("Total weight for team 1: %d\n", sum1);
    printf("Total weight for team 2: %d\n", sum2);
    
    return 0;
}
```



# 3 Combining logic conditions using the logical AND and OR

## 3.1 Combine logical conditions using AND

```c
#include <stdio.h>
int main(void) {
    int sunny = 1;
    int vacation = 1;
    int sunAndVacation = sunny && vacation;
    // 1 && 1 : 1,  1 && 0 : 0, 0 && 1 : 0, 0 && 0 : 0
    if (sunAndVacation) {
        printf("Yeah!!\n");
    } else {
        printf("Too bad!\n");
    }
    return 0;
}
```



## 3.2 Combine logical conditions using OR

```c
#include <stdio.h>
int main(void) {
    int sunny = 0;
    int vacation = 0;
    int sunORvacation = sunny || vacation;
    //1||1:1 1||0:1 0||1:1 0||0:0
    if(sunORvacation){
        printf("Going well: it is sunny OR I am on vacation OR both!\n");
    }else{
        printf("Not going well: it is NEITHER sunny NOR am I on vacation!\n");
    }
    return 0;
}
```



## 3.3 Activity: more complex if statements: costly hotel rooms

The hostel in which you stop for the night changes  its prices according to the age of the customer and the weight of their  luggage. The rules are not very clear, so you decide to write a small  program that will easily allow you and your travel companions to know  the price of one night.

One room costs nothing if you are 60 (the age of the innkeeper), or 5 dollars if you are less than 10 years old. For  everyone else, the cost is 30 dollars plus an additional 10 dollars if  you bring more than 20 pounds of luggage. Your program should read the  customer's age first, then the weight of their luggage, then output the  price they have to pay.

### Example

#### Input:

```
22
25
```

#### Output:

```
40
```



我的程序：

```c
#include <stdio.h>
int main(void){
    int age, weight, money;
    scanf("%d%d", &age, &weight);
    if (age == 60){
        money = 0;
    } else if (age < 10){
        money = 5;
    } else if (weight <= 20) {
        money = 30;
    } else {
        money = 40;
    }
    printf("%d", money);
   
    return 0;
}
```





# 4 Negating a logic condition using the logic 

# operator NOT

## 4.1 Negate a logical condition using NOT

```c
#include <stdio.h>
int main(void) {
    int sunny = 0; // 0: cloudy, other value (1 for example): sunny
    int vacation = 0; // 0: working , other value (1 for example): vacation
    int NOTsunnyANDNOTvacation = !sunny && !vacation;
    if (NOTsunnyANDNOTvacation){
        printf("It's neither sunny nor am I on vacation!\n");
    }
    return 0;
}
```



## 4.2 Branch using complex logical conditions

初始版：

```c
#include <stdio.h>
int main(void) {
    int age;
    printf("What is your age?\n");
    scanf("%d",&age);
    int isAdult = age >= 18;
    int isSenior = age >= 65;
    int isInTheWorkForce = isAdult && !isSenior;
    if(isInTheWorkForce){
        printf("You are in the labor force\n");
    }else{
        printf("You are not in the labor force\n");
    }
    return 0;
}
```



最终优化版：

```c
#include <stdio.h>
int main(void) {
    int age;
    printf("What is your age?\n");
    scanf("%d",&age);
    if(age >= 18 && !(age >= 65)){
        printf("You are in the labor force\n");
    }else{
        printf("You are not in the labor force\n");
    }
    return 0;
}
```



## 4.3 Activity: if statements, name that tree

As you cross a forest you can't help but admire the  nature around you including the many species of trees. Despite your  interest, you are a very unskilled botanist and have a lot of trouble  identifying different trees. A friend gives you some guidance and you  decide to write a program that will give you the name of the tree based  on its characteristics.

There are 4 types of trees:

the "Tinuviel" is **5 meters high or less** and its leaves are composed of **8 or more leaflets**

the "Calaelen" is **10 meters high or more** and its leaves are composed of **10 or more leaflets**

the "Falarion" is **8 meters high or less** and its leaves are composed of **5 or fewer leaflets**

the "Dorthonion" is **12 meters tall** **or more** and its leaves are composed of **7 or fewer leaflets**

Your program should read the height and the number  of leaflets of a given tree (both integers), and should be able to  determine and display the name of the corresponding tree. If the height and number of leaflets does not match any of the tree type  descriptions, your program should display "Uncertain".

### Example 1

#### Input

```
12
12
```

#### Output

```
Calaelen
```

### Example 2

#### Input

```
4
9
```

#### Output

```
Tinuviel
```

### Example 3

#### Input

```
4
6
```

#### Output

```
Uncertain
```



我的程序：

```c
#include <stdio.h>
int main(void){
    int height, number;
    scanf("%d%d", &height, &number);
    if (height <= 5 && number >= 8){
        printf("Tinuviel");
    } else if (height >= 10 && number >= 10){
        printf("Calaelen");
    } else if (height <= 8 && number <= 5){
        printf("Falarion");
    } else if (height >= 12 && number <= 7){
        printf("Dorthonio");
    } else {
        printf("Uncertain");
    }
    return 0;
}
```

