[TOC]

# 1 Define structures

## 1.1 Define and use structures

```c
#include <stdio.h>

struct student{
    char firstName[30];
    char lastName[30];
    int birthYear;
    double aveGrade;
};

int main(void) {
	//! showMemory(start=65520)
    struct student me = {"Petra", "Bonfert-Taylor", 1989, 3.5};
    struct student you = {"Remi", "Sharrock", 2005, 3.5};
    printf("Names: %s %s, %s %s\n", me.firstName, me.lastName, you.firstName, you.lastName);
    printf("Year of birth: %d\n", me.birthYear);
    printf("Average grade: %.2lf\n", me.aveGrade);
	return 0;
}
```



# 2 Access and modify structures

## 2.1 Access and modify structure’s members with the dot operator

```c
#include <stdio.h>

struct student{
	char firstName[30];
	char lastName[30];
	int birthYear;
	double aveGrade;
};

int main(void) {
    //! showMemory(start=65520)
    struct student learner;
    printf("First name: ");
    scanf("%s", learner.firstName);
    printf("Last name: ");
    scanf("%s", learner.lastName);
    printf("Year of birth:");
    scanf("%d", &learner.birthYear);
    printf("Average grade: ");
    scanf("%lf", &learner.aveGrade);
    
    printf("Name: %s %s\n", learner.firstName, learner.lastName);
	printf("Year of birth: %d\n",learner.birthYear);
	printf("Average grade: %.2lf\n",learner.aveGrade);
    
	return 0;
}
```



# 3 Pass structures to functions

## 3.1 Pass structures to functions directly

```c
#include <stdio.h>

struct student{
	char firstName[30];
	char lastName[30];
	int birthYear;
	double aveGrade;
};
void printStudent(struct student stud);
int main(void) {
	//! showMemory(start=65520)
	struct student me={"Petra", "Bonfert-Taylor", 1989, 3.5};
	struct student you={"Remi", "Sharrock", 2005, 3.5};
	
	printStudent(me);
	printStudent(you);
	return 0;
}

void printStudent(struct student stud){
  printf("Name: %s %s\n", stud.firstName, stud.lastName);
	printf("Year of birth: %d\n",stud.birthYear);
	printf("Average grade: %.2lf\n",stud.aveGrade);
}
```



## 3.2 Pass structures to functions with pointers

```c
#include <stdio.h>

struct student{
	char firstName[30];
	char lastName[30];
	int birthYear;
	double aveGrade;
};

void printStudent(struct student);
void readStudent(struct student *studptr);

int main(void) {
   //! showMemory(start=65520)
    struct student me;
    readStudent(&me);
    printStudent(me);
    return 0;
}

void readStudent(struct student *studptr) {
    printf("\nEnter a new student record: \n");
    printf("First name: ");
    scanf("%s", (*studptr).firstName);
    printf("Last name: ");
    scanf("%s", (*studptr).lastName);
    printf("Birth year: ");
    scanf("%d", &(*studptr).birthYear);
    printf("Average grade: ");
    scanf("%lf", &(*studptr).aveGrade);
}

void printStudent(struct student stud) {
    printf("Name: %s %s\n", stud.firstName, stud.lastName);
    printf("Year of birth: %d\n",stud.birthYear);
    printf("Average grade: %.2lf\n",stud.aveGrade);
}
```



## 3.3 Activity: pass structures to functions

You'd like to implement a date feature in the C  programming language. To this end you are provided with a structure  definition, a main function, and two function prototypes: "readDate()"  and "printDate()". All that is left for you to do is to write these two  functions.

Here are the exact specifications:

The function readDate() should read 3 integers from  the user input. The first integer is the year (a 4-digit number), the  second integer is the month, and the third integer is the day of the  date being read. The function should store these three numbers in the  appropriate parts of the structure being passed into it.

The function printDate() should print the date  stored in the variable passed into it in the following format:  mm/dd/yyyy with a new line afterwards. So the month should be printed  with two digits (01, 02, 03, ..., 11, 12), the day should be printed as  two digits (01, 02, 03, ..., 30, 31), and the year should be printed as a 4-digit number.

You should not modify the provided code.

 

**Examples**

**Input:**

```
2018 10 2
```

**Output: **

```
10/02/2018
```

 

**Provided Code:**

```c
#include <stdio.h>

struct date {
        int year;
        int month;
        int day;
    };

void readDate(struct date *);
void printDate(struct date);

int main(void) {
	struct date today;
	readDate(&today);
	printDate(today);
	return 0;
}
```



**我的程序：**

```c
#include <stdio.h>

struct date {
        int year;
        int month;
        int day;
    };

void readDate(struct date *);
void printDate(struct date);

int main(void) {
	struct date today;
	readDate(&today);
	printDate(today);
	return 0;
}

void readDate(struct date *todayptr){
    scanf("%d %d %d", &(*todayptr).year, &(*todayptr).month, &(*todayptr).day);
}

void printDate(struct date today){
    printf("%02d/%02d/%04d", today.month, today.day, today.year);
}
```



补充：
以输出整型数值为例，要输出整型数字占m位，不足部分补0，可以写作：printf("%0md", var)；

其中m为正整数。
当输出的实际位数超过m时，会按照实际位数输出，否则左边补0，凑齐m位输出。
如：
printf("%04d", 20); 会输出0020；
printf("%08d",123); 会输出00000123；
而printf("%03d",1234);会按照本身的长度输出，即1234。这时的03控制无效。 



# 4 Work with structures

## 4.1 Access and modify structure’s members with the arrow operator

```c
#include <stdio.h>

struct student{
	char firstName[30];
	char lastName[30];
	int birthYear;
	double aveGrade;
};
void printStudent(struct student);
void readStudent(struct student *studptr);
int main(void) {
   //! showMemory(start=65520)
    struct student me;
    readStudent(&me);
    printStudent(me);
	return 0;
}

void readStudent(struct student *studptr) {
    printf("\nEnter a new student record: \n");
    printf("First name: ");
    scanf("%s", studptr->firstName);
    printf("Last name: ");
    scanf("%s", studptr->lastName);
    printf("Birth year: ");
    scanf("%d", &studptr->birthYear);
    printf("Average grade: ");
    scanf("%lf", &studptr->aveGrade);
}

void printStudent(struct student stud) {
    printf("Name: %s %s\n", stud.firstName, stud.lastName);
	printf("Year of birth: %d\n",stud.birthYear);
	printf("Average grade: %.2lf\n",stud.aveGrade);
}
```



解析：

```scanf("%s", (*studptr).firstName);```

不需要加&，因为这里是string；

stuptr是pointer，所以写成\*stuptr，指对应的变量；

.firstName是对应到具体的组分。



这样子太复杂了，所以换成->的格式。结果是一样的。



## 4.2 Get the size of a structure in memory

```c
#include <stdio.h>

struct student{
	char firstName[5];
	char lastName[5];
	int birthYear;
	double aveGrade;
};

int main(void) {
    //! showMemory(start=65520)
	struct student me;
    printf("Size of struct student is %zu.\n", sizeof(struct student));
    printf("Size of firstName is %zu.\n", sizeof(me.firstName));
    printf("Size of lastName is %zu.\n", sizeof(me.lastName));
    printf("Size of birthYear is %zu.\n", sizeof(me.birthYear));
    printf("Size of aveGrade is %zu.\n", sizeof(me.aveGrade));

	return 0;
}
```



输出：

```
Size of struct student is 22.                                                   
Size of firstName is 5.                                                         
Size of lastName is 5.                                                          
Size of birthYear is 4.                                                         
Size of aveGrade is 8. 
```



此处的大小是22，但有的compiler的结果是24。

这是因为各个compiler不同，可能会提供更多的空格。



## 4.3 Activity: manipulate structures with functions

In this problem you will continue developing the  data feature which you started implementing in the previous problem. You will implement a "tomorrow" feature in the C programming language via a function called "advanceDay()". The function advanceDay() should take  as input a date (stored in a struct date) and return the date of the  following day. You do not have to take into account leap years (although you may if you wish to). That is, it is okay for your function to  always return March 1 as the day following February 28, no matter the  year.

You are provided with a familiar date structure  definition, a main function as well as the function prototypes for the  readDate(), printDate(), and advanceDate() functions. Do not modify any  of the given code. Simply add your function definitions underneath the  main() function. For the readDate() and printDate() functions you may  simply copy and paste the code you developed in the previous task. 

**Examples**

**Input:**

```
2018 10 2
```

**Output: **

```
10/02/2018                                                                      

10/03/2018
```

 

**Input:**

```
2018 10 31
```

**Output: **

```
10/31/2018                                                                      

11/01/2018
```

 

**Input:**

```
2018 11 30
```

**Output: **

```
11/30/2018                                                                      

12/01/2018                                                                      
```

 

**Input:**

```
2018 12 31
```

**Output: **

```
12/31/2018                                                                      

01/01/2019
```

**Provided code**

```c
#include <stdio.h>

struct date {
        int year;
        int month;
        int day;
    };

/* function prototypes */
void printDate(struct date);
void readDate(struct date *);
struct date advanceDay(struct date); 

int main(void) {
	struct date today, tomorrow;
	readDate(&today);
	printDate(today);
	tomorrow = advanceDay(today);
	printDate(tomorrow);
	return 0;
}

/* add your function definitions here */
```



**我的程序：**

```c
#include <stdio.h>

struct date {
        int year;
        int month;
        int day;
    };

/* function prototypes */
void printDate(struct date);
void readDate(struct date *);
struct date advanceDay(struct date); 

int main(void) {
	struct date today, tomorrow;
	readDate(&today);
	printDate(today);
	tomorrow = advanceDay(today);
	printDate(tomorrow);
	return 0;
}

/* add your function definitions here */
void readDate(struct date *todayptr){
    scanf("%d %d %d", &todayptr->year, &todayptr->month, &todayptr->day);
    //scanf("%d %d %d", &(*todayptr).year, &(*todayptr).month, &(*todayptr).day);
}

void printDate(struct date today){
    printf("%02d/%02d/%04d\n", today.month, today.day, today.year);
}

struct date advanceDay(struct date today){
    int numberDay;
    if (today.month == 1 && today.month == 3 && today.month == 5 && today.month == 7 && today.month == 8 && today.month == 10 && today.month == 12){
        numberDay = 31;
    } else if (today.month == 2){
        numberDay = 28;
    } else {
        numberDay = 30;
    }
    
    if (today.month == 12 && today.day == 31){
        today.year += 1;
        today.month = 1;
        today.day = 1;
    } else if (today.day == numberDay){
       today.month += 1;
       today.day = 1;
    } else {
        today.day += 1;
    }
    
    return today;
}
```