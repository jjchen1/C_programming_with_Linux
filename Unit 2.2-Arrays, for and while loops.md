[TOC]

# 1 Using arrays of integers

## 1.1 Store integers in an array

```c
#include <stdio.h>
int main(void) {
    int array[3]; // creates space to hold three integers
    array[0] = 18;
    array[1] = 137;
    array[2] = 8;
    printf("First element is %d.\n", array[0]);
    printf("Second element is %d.\n", array[1]);
    printf("Third element is %d.\n", array[2]);
    return 0;
}
```



## 1.2 Assign array elements from user input

```c
#include <stdio.h>
int main(void){
    int array[3];
    int readValue = 0;
    int cellNumber = 0;
    int i = 0;
    for(i = 0 ; i < 3 ; i++){
        printf("Enter a value:");
        scanf("%d", &readValue);
        array[cellNumber] = readValue;
        printf("Cell number %d contains %d\n", cellNumber, array[cellNumber]);
        cellNumber = cellNumber + 1;
    }
    return 0;
}
```

（我觉得有点啰嗦，直接写入数组即可。）



## 1.3 Activity: store recipe ingredients in an array

Your grandparents gave you a fantastic cooking  recipe but you can never remember how much of each ingredient you have  to use! There are 10 ingredients in the recipe and the quantities needed for each of them are given as input (in grams). Your program must read  10 integers (the quantities needed for each of the ingredients, in  order) and store them in an array. It should then read an integer which  represents an ingredient's ID number (between 0 and 9), and output the  corresponding quantity.

**Examples**

**Input:**

```
500 180 650 25 666 42 421 1 370 211
3
```

**Output: **

```
25
```



**我的程序：**

```c
#include <stdio.h>
int main(void){
    int array[10];
    int i,number;
    for (i=0; i<10; i++){
        scanf("%d", &array[i]);
    }
    scanf("%d", &number);
    printf("%d", array[number]);
    return 0;
}
```



# 2 Repeating instructions with a FOR loop

## 2.1 Explore details of the for loop

```c
#include <stdio.h>
int main(void) {
    int i;
    // i++ is short for i = i+1
    for (i = 3; i>0; i = i-1) {
        printf("i has the value %d.\n", i);
    }
    return 0;
}
```



## 2.2 Store doubles in an array

```c
#include <stdio.h>
int main(void){
    double array[3];
    double readValue = 0.0;
    int cellNumber = 0;
    int i = 0;
    for(i=0;i<3;i++){
        printf("Enter a decimal value:");
        scanf("%lf",&readValue);
        array[cellNumber] = readValue;
        printf("Cell number %d contains %.2lf\n", cellNumber, array[cellNumber]);
        cellNumber = cellNumber + 1;
    }
    return 0;
}
```



## 2.3 Activity: use an array to balance weights

You are responsible for a rail convoy of goods  consisting of several boxcars. You start the train and after a few  minutes you realize that some boxcars are overloaded and weigh too  heavily on the rails while others are dangerously light. So you decide  to stop the train and spread the weight more evenly so that all the  boxcars have exactly the same weight (without changing the total  weight). For that you write a program which helps you in the  distribution of the weight.

Your program should first read the number of cars to be weighed (integer) followed by the weights of the cars (doubles).  Then your program should calculate and display how much weight to add or subtract from each car such that every car has the same weight. The  total weight of all of the cars should not change. These additions and  subtractions of weights should be displayed with one decimal place.

You may assume that there are no more than 50 boxcars. 

**Examples**

In this example, there are 5 boxcars with different  weights summing to 110.0. The ouput shows that we are modifying all the  boxcars so that they each carry a weight of 22.0 (which makes a total of 110.0 for the entire train). So we remove 18.0 for the first boxcar, we add 10.0 for the second, we add 2.0 for the third, etc.

**Input:**

```
5
40.0
12.0
20.0
5.0
33.0
```

**Output: **

```
-18.0
10.0
2.0
17.0
-11.0
```



**我的程序：**

```c
#include <stdio.h>
int main(void){
    int number, i;
    double weight[50];
    double each;
    scanf("%d", &number);
    each =110/number;
    
    for (i=0; i<number; i++){
        scanf("%lf", &weight[i]);
    }
    
    for (i=0; i<number; i++){
        printf("%.1lf\n", each-weight[i]);
    }
    
    return 0;
}
```



# 3 Using an IF statement inside a FOR loop

## 3.1 Find the largest array element

```c
#include <stdio.h>
int main(void) {
    //! showArray(ages, cursors=[i])
    int ages[10];
    int i;
    int ageMax = 0;
    for (i=0; i<10; i++) {
        scanf("%d", &ages[i]);
        if (ages[i] > ageMax) {
            ageMax = ages[i];
        }
    }
    printf("The maximum age is %d.\n", ageMax);
    return 0;
}

```



## 3.2 Compute with arrays

```c
#include <stdio.h>
int main(void) {
    //! showArray(ages, cursors=[i])
    int ages[10];
    int i;
    int ageMax = 0;
    for (i=0; i<10; i++) {
        scanf("%d", &ages[i]);
        if (ages[i] > ageMax) {
            ageMax = ages[i];
        }
    }
    printf("The maximum age is %d.\n", ageMax);
    printf("Age differences with the eldest person:\n");
    for(i=0;i<10;i++){
        printf("%d:%d ", ages[i],ageMax-ages[i]);
    }
    return 0;
}
```



## 3.3 Activity: array computation

You plan to make a delicious meal and want to take  the money you need to buy the ingredients. Fortunately you know in  advance the price per pound of each ingredient as well as the exact  amount you need. The program should read in the number of ingredients  (up to a maximum of 10 ingredients), then for each ingredient the price  per pound. Finally your program should read the weight necessary for the recipe (for each ingredient in the same order). Your program should  calculate the total cost of these purchases, then display it with 6  decimal places.

**Examples**

There are 4 ingredients and they all have a  different price per pound: 9.90, 5.50, 12.0, and 15.0. You must take  0.25 lbs of the first, 1.5 lbs of the second, 0.3 lbs of the third and 1 lb of the fourth. It will cost exactly $29.325000.

**Input:**

```
4
9.90 5.50 12.0 15.0
0.250 1.5 0.300 1.0
```

**Output: **

```
29.325000
```



**我的程序：**

```c
#include <stdio.h>
int main(void){
    int number, i;
    double price[10], weight[10];
    double money;
    money = 0.0;
    scanf("%d", &number);
    
    for (i=0; i<number; i++){
        scanf("%lf", &price[i]);
    }
    
    for (i=0; i<number; i++){
        scanf("%lf", &weight[i]);
        money += price[i]*weight[i];
    }
    
    printf("%.6lf", money);
    return 0;
}
```



# 4 Nesting IF and FOR

## 4.1 Nest if and for

```c
#include <stdio.h>
int main(void) 
{
    int target;
    int i;
    printf("Please enter a target number: ");
    scanf("%d", &target);
    if (target >= 0) 
    {
        for (i=0; i<target; i++) 
        {
            if (i%2) 
            {
                printf("%d ", i);
            }
        }
    } 
    else 
    {
        printf("Nothing to do!\n");
    }
    return 0;
}

```



## 4.2 Activity: branch inside a loop, how many big cities?

You want to determine the number of cities in a  given region that have a population strictly greater than 10,000. To do  this, you write a program that first reads the number of cities in a  region as an integer, and then the populations for each city one by one  (also integers).

**Examples**

**Input:**

```
6
1000
5000
15000
4780
0
23590
```

**Output: **

```
2
```



**我的程序：**

```c
#include <stdio.h>
int main(void){
    int number, i, calc;
    int population[100];
    calc = 0;
    scanf("%d", &number);
    
    for (i=0; i<number; i++){
        scanf("%d", &population[i]);
        if (population[i] > 10000){
            calc += 1;
        }
    }
    
    printf("%d", calc);
    return 0;
}
```



# 5 Repeating inside repetition

## 5.1 Nest FOR loops

```c
#include <stdio.h>
int main(void){
    int nbThrows = 0;
    int nbDice = 0;
    int diceValue = 0;
    int throwSum = 0;
    int throw = 0;
    int dice = 0;
    scanf("%d %d", &nbThrows, &nbDice);
    for(throw = 0; throw<nbThrows; throw++){
        for(dice = 0; dice<nbDice; dice++){
            scanf("%d", &diceValue);
            throwSum = throwSum + diceValue;
        }
        printf("throw %d sum equals %d\n", throw, throwSum);
        throwSum = 0;
    }
    return 0;
}
```



## 5.2 Activity: print a square of stars using nested loops

Create a program that displays on the screen a square of n x n stars, with the integer n given as an input.

**Examples**

**Input:**

```
5
```

**Output: **

```
*****
*****
*****
*****
*****
```


**Input:**

```
3
```

**Output: **

```
***
***
***
```



**我的程序：**

```c
#include <stdio.h>
int main(void){
    int number, i, j;
    scanf("%d", &number);
    
    for (i=0; i<number; i++){
        for (j=0; j<number; j++){
            printf("*");
        }
        printf("\n");
    }
    
    return 0;
}
```



# 6 Repeating using a WHILE loop

## 6.1 Repeat instructions using a while loop - introduction

```c
#include <stdio.h>
int main(void) {
    int diceValue;
    int notSix;
    scanf("%d", &diceValue);
    notSix = diceValue != 6;
    while (notSix) {
        scanf("%d", &diceValue);
        notSix = diceValue != 6;
    }
    return 0;
}
```



## 6.2 Repeat using a while loop

```c
#include <stdio.h>
int main(void) {
    int diceValue = 0;
    int nbThrows = 0;
    scanf("%d", &diceValue);
    while(diceValue != 6){
        scanf("%d", &diceValue);
        nbThrows = nbThrows + 1;
    }
    printf("We needed %d throws to get the value 6\n", nbThrows+1);
    return 0;
}
```



## 6.3 Activity: compute budget using a while loop

Much of the work of a university administration (in  addition to managing teachers, researchers, students, courses, etc.) is  to ensure the proper functioning of the university and in particular  that the accounting job is well done. Once a year, an annual report of  expenditures must be made.

All expenses for the year have been recorded and  classified in a multitude of files and the sum of all these expenses  must now be calculated. But no one knows exactly how many different  expenses have been made in the past year!

Your program will have to read a sequence of  positive integers and display their sum. We do not know how many  integers there will be, but the sequence always ends with the value -1  (which is not an expense, just an end marker).

**Examples 1**

**Input:**

```
1000
2000
500
-1
```

**Output: **

```
3500
```

**Examples 2**

**Input:**

```
-1
```

**Output: **

```
0
```

**Examples 3**

**Input:**

```
150
250
350
4500
240
120
-1
```

**Output: **

```
5610
```



**我的程序：**

```c
#include <stdio.h>
int main(void){
    int expense, isNotMinus1;
    int all=0;
    scanf("%d", &expense);
    isNotMinus1 = expense != -1;
    while (isNotMinus1){
        all += expense;
        scanf("%d", &expense);
        isNotMinus1 = expense != -1;
    }
    
    printf("%d", all);
    return 0;
}
```



# 7 Efficiently using a WHILE loop

## 7.1 Check a logic statement to continue looping

```c
#include <stdio.h>
int main(void) {
    int signaturesNeeded = 1000;
    int day = 0;
    int newSignatures = 3;
    int totalSignatures = 3;
    while (totalSignatures < 1000) {
        day++;
        newSignatures = 2*newSignatures;
        printf("Day %d: %d new signatures! ", day, newSignatures);
        totalSignatures = totalSignatures + newSignatures;
        printf("Total: %d\n", totalSignatures);
    }
    return 0;
}
```



## 7.2 Activity: controlling an epidemic

In order to be able to better fight various  epidemics in a region, the department of medicine of a major university  has launched a large study. Researchers are interested in how fast an  epidemic spreads, and therefore the speed at which health measures must  be put in place. Your program should first read an integer representing  the total population of the area. Knowing that a person was infected on  day 1 and that each infected person contaminates two new people every  day, you must calculate the day at which the entire population of the  area will be infected. 

**Examples**

For a total population of 3 inhabitants, on day 1 a  single person is infected. The next day, that person contaminates 2 new  people so there are 3 infected people in total. This is the entire  population, so it takes 2 days to contaminate the entire population.

**Input:**

```
3
```

**Output: **

```
2
```

For a total population of 10 inhabitants, on day 1 a single person is infected. This is followed by 2 new people on the  second day for a total of 3 infected people. On the third day, 6 new  people are infected for a total of 9 infected people. On the fourth day  the last of the 10 people is infected (though the epedemic had the  potential to infect 18 people on the fourth day) so your program should  output '4'.

**Input:**

```
10
```

**Output: **

```
4
```



**我的程序：**

```c
#include <stdio.h>
int main(void){
    int population, notAll;
    int infectedPeople = 1;
    int numberDay = 1;
    scanf("%d", &population);
    notAll = infectedPeople < population;
    
    while (notAll){
        infectedPeople *= 3;
        numberDay +=1;
        notAll = infectedPeople < population;
    }
    
    printf("%d", numberDay);
    return 0;
}
```



# 8 Practicing WHILE loops

## 8.1 Activity: guess my number

We would like you to develop a program capable of  making a child play automatically the game of "more or less" -- the  child must try to guess a secret number. The program should respond to  each guess with "it is more" or "it is less" until the child finds the  right number.

Your program must first read an integer indicating  the number that the child will have to find during the game. Next the  program should repeatedly read the player's guesses and display the text "it is more" if the child has submitted a smaller number or "it is  less" if they have submitted a larger number. Once the correct number is reached, the program should print "Number of tries needed:" followed by a new line and the integer number of tries that it took the guesser.

**Examples 1**

**Input:**

```
5
1 2 3 4 5
```

**Output: **

```
it is more
it is more
it is more
it is more
Number of tries needed:
5
```

**Examples 2**

**Input:**

```
10
5 15 8 12 11 10
```

**Output: **

```
it is more
it is less
it is more
it is less
it is less
Number of tries needed:
6
```



**我的程序：**

```c
#include <stdio.h>
int main(void){
    int rightNumber, guessNumber;
    int numberOfTry = 0;
    int isContinue = 1;
    scanf("%d", &rightNumber);
    
    while (isContinue){
        scanf("%d", &guessNumber);
        numberOfTry += 1;
        if (guessNumber > rightNumber){
            printf("it is less\n");
        } else if (guessNumber < rightNumber){
            printf("it is more\n");
        } else {
            printf("Number of tries needed:\n");
            printf("%d", numberOfTry);
            isContinue = 0;
        }
    }
    
    return 0;
}
```



## 8.2 Activity: monitoring a chemical experiment

University chemists have developed a new process for the manufacturing of a drug that heals wounds extremely quickly. The  manufacturing process is very lengthy and requires monitoring the  chemicals at all times, sometimes for hours! Entrusting this task to a  student is not possible; students tend to fall asleep or not pay close  attention after a while. Therefore you need to program an automatic  device to monitor the manufacturing of the drug. The device measures the temperature every 15 seconds and provides these measurement to your  program. 

Your program should first read two integers  representing the minimum and maximum safe temperatures. Next, your  program should continuously read temperatures (integers) that are being  provided by the device. Once the chemical reaction is complete the  device will send a value of -999, indicating to you that temperature  readins are done. For each recorded temperature that is in the correct  range (it could also be equal to the min or max values), your program  should display the text "Nothing to report". But as soon as a  temperature reaches an unsafe level your program must display the text  "Alert!" and stop reading temperatures (although the device may continue sending temperature values).

**Examples**

**Input:**

```
10 20
15 10 20 0 15 -999
```

**Output: **

```
Nothing to report
Nothing to report
Nothing to report
Alert!
```

 

**Input:**

```
0 100
15 50 75 -999
```

**Output: **

```
Nothing to report
Nothing to report
Nothing to report
```



**我的程序：**

```c
#include <stdio.h>
int main(void){
    int minTemperature, maxTemperature, temperature[100];
    int i = 0;
    int isContinue = 1;
    scanf("%d%d", &minTemperature, &maxTemperature);
    
    while (isContinue){
        scanf("%d", &temperature[i]);
        if (temperature[i] == -999){
            isContinue = 0;            
        } else {
            i += 1;
        }    
    }
    
    for (i=0; i<100; i++){
        if (temperature[i] >= minTemperature && temperature[i] <= maxTemperature){
            printf("Nothing to report\n");
        } else if (temperature[i] == -999){
            i = 100;
        } else {
            printf("Alert!");
            i = 100;
        }
    }

    return 0;
}
```