#  1 Creating a single node

## 1.1 Create a node of a linked list

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit * next;
};
struct digit * createDigit(int dig);
int main(void) {
    //! stack=showMemory(start=65520, showcursor[numberptr])
    struct digit * numberptr;
    int digitToStore = 5;
    numberptr = createDigit(digitToStore);
    printf("We are storing the digit %d and the pointer %p at memory location %p.\n", numberptr->num, numberptr->next, numberptr);
    free(numberptr);
    return 0;
}

struct digit * createDigit(int dig) {
    //! heap=showMemory(start=330, cursors=[ptr])
    struct digit *ptr;
    ptr = (struct digit *) malloc(sizeof(struct digit));
    ptr->num = dig;
    ptr->next = NULL;
    return ptr;
}
```



## 1.2 Activity: create a node to store student data

You would like to store student data (for each  student, their name and age) in a linked list of students. You are given the following structure to store each student's information. Please do  not modify this structure:

```c
struct student {
      char name[50];
      int age;
      struct student *next;
};
```

Your first task is to write a function  createStudent() that takes as inputs a string (namely a student's name)  and an integer (their age) and that returns a pointer to a struct  student which stores this information. Your function should dynamically  allocate the memory required for this struct student and then write the  student's name and age into this newly allocated memory. 

You are given the createStudent() function prototype and a main() function to test your code, please do not modify these:

```c
struct student *createStudent(char studentName[], int studentAge);

int main(void) {
    struct student *studptr;
    int myAge;
    char myName[50];
    scanf("%s %d", myName, &myAge);
    studptr = createStudent(myName, myAge);
    printf("New student created: %s is %d years old.\n", studptr->name, studptr->age);
    free(studptr);
    return 0;
}
```

### Examples

#### Input:

```
Petra 25
```

#### Output:

```
New student created: Petra is 25 years old.   
```

#### Input:

```
Remi 18
```

#### Output:

```
New student created: Remi is 18 years old.   
```



This task offers 1 hint :

**Hint 1 :**

It may be useful to create a function copyStr() which copies one string to another string.



我的程序（错误）：

```c
#include <stdio.h>
#include <stdlib.h>

struct student {
      char name[50];
      int age;
      struct student *next;
};

struct student *createStudent(char studentName[], int studentAge);

// Write other function prototypes here (if any)
char copyStr(char str[]);

int main(void) {
    struct student *studptr;
    int myAge;
    char myName[50];
    scanf("%s %d", myName, &myAge);
    studptr = createStudent(myName, myAge);
    printf("New student created: %s is %d years old.\n", studptr->name, studptr->age);
    free(studptr);
    return 0;
}

// Write your createStudent function here (and any other functions you see fit)
struct student *createStudent(char studentName[], int studentAge){
    struct student * ptr;
    ptr = (struct student *) malloc(sizeof(struct student));
    ptr->name = copyStr(studentName[]);
    ptr->age = studentAge;
    ptr->next = NULL;
    return ptr;
}

char copyStr(char str[]){
    int i=0;
    char str2[50];
    while (str[i]!='\0') {
        str2[i] = str[i];
        i++;
    }
    str2[i] = '\0';
    return str2;
}
```



错误提示：

```
 Compilation result :

341411970576882947.c: In function ‘createStudent’:
341411970576882947.c:30:37: error: expected expression before ‘]’ token
     ptr->name = copyStr(studentName[]);
                                     ^
341411970576882947.c: In function ‘copyStr’:
341411970576882947.c:44:5: warning: return makes integer from pointer without a cast
     return str2;
     ^
341411970576882947.c:44:5: warning: function returns address of local variable [-Wreturn-local-addr]
```



链接：

C语言中，为什么字符串可以赋值给字符指针变量https://blog.csdn.net/yichu5074/article/details/81701850



下一节，提供了正确代码：

```c
struct student *createStudent(char studentName[], int studentAge) {
    struct student *ptr;
    ptr = (struct student *) malloc(sizeof(struct student));
    copyStr(studentName, ptr->name);  /*类似交换函数swap(x, y)，而不是返回值*/
    ptr->age = studentAge;
    ptr->next = NULL;
    return ptr;
}

void copyStr(char *source, char *target) {
    int i = 0;
    while (source[i]!='\0') {
        target[i] = source[i];
        i++;
    }
    target[i] = '\0';
}
```



# 2 Linking nodes

## 2.1 Append a node to a linked list

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit * next;
};
struct digit * createDigit(int dig);
struct digit * append(struct digit * end, struct digit * newDigitptr);
int main(void) {
    //! stack=showMemory(start=65520,cursors=[start,newDigitptr,end,tmp])
    struct digit *start, *newDigitptr, *end, *tmp;
    int first = 5;
    int second = 3;
    int third = 7;
    start = createDigit(first);
    end = start;
    newDigitptr = createDigit(second);
    end = append(end, newDigitptr);
    newDigitptr = createDigit(third);
    end = append(end, newDigitptr);
    // free needs to be added  here
    tmp = start->next;
    free(start);
    start = tmp;
    tmp = start->next;
    free(start);
    free(tmp);
    return 0;
}

struct digit * append(struct digit * end, struct digit * newDigitptr) {
    //! heap=showMemory(start=260, cursors=[end,newDigitptr])
    end->next = newDigitptr;
    end = newDigitptr;
    return(end);
}

struct digit * createDigit(int dig) {
    //! heap=showMemory(start=260, cursors=[ptr])
    struct digit *ptr;
    ptr = (struct digit *) malloc(sizeof(struct digit));
    ptr->num = dig;
    ptr->next = NULL;
    return ptr;
}
```



## 2.3 Activity: append a node with student data

In this task you will continue working on the linked list of students in which you would like to store, for each student,  their name and age. As before you are provided with some code that you  should not modify:

- A structure definition for the storage of each student's information.
- A main() function to test your code. 
- Prototypes for the functions createStudent() (from the previous task) and append() (from the current task).

You will need the function definition (from the  previous task) for createStudent(), as well as any other functions you  added, such as copyStr() for example. If you were unable to solve the  previous task you have the option to be given the code for the  createStudent() function (see the quiz preceding this task) so that you  can work on the current task.

Your new task is to write a function append() which  takes as input two pointers: the first pointer holds the address of the  current end of the linked list of students, the second pointer points to a newly created student. Your function should append this new student  to the linked list and return the address (a struct student *) of the  new end of the list. 

### Provided code

```c
#include <stdio.h>
#include <stdlib.h>

struct student {
      char name[50];
      int age;
      struct student *next;
};

struct student *createStudent(char studentName[], int studentAge);
struct student *append(struct student * end, struct student * newStudptr); 
/* add other prototypes here if needed */

int main(void) {
    struct student *start, *newStudptr, *end, *tmp;
    int ageP, ageR, ageM;

    scanf("%d %d %d", &ageP, &ageR, &ageM);
    start = createStudent("Petra", ageP);
    end = start;
    newStudptr = createStudent("Remi", ageR);
    end = append(end, newStudptr);
    newStudptr = createStudent("Mike", ageM);
    end = append(end, newStudptr);

    printf("%s is %d years old.\n", start->name, start->age);
    printf("%s is %d years old.\n", start->next->name, start->next->age);
    printf("%s is %d years old.\n", start->next->next->name, start->next->next->age);

    tmp = start->next;
    free(start);
    start = tmp;
    tmp = start->next;
    free(start);
    free(tmp);

    return 0;
}

/* Place your function definitions here. Be sure to include the definition for 
   createStudent() and any other functions you created for the previous task. */
```

### Example

#### Input: 

```
25 18 32
```

#### Output: 

```
Petra is 25 years old.
Remi is 18 years old.
Mike is 32 years old.
```



我的程序：

```c
#include <stdio.h>
#include <stdlib.h>

struct student {
      char name[50];
      int age;
      struct student *next;
};

struct student *createStudent(char studentName[], int studentAge);
struct student *append(struct student * end, struct student * newStudptr); 
/* add other prototypes here if needed */
void copyStr(char *source, char *target);

int main(void) {
    struct student *start, *newStudptr, *end, *tmp;
    int ageP, ageR, ageM;

    scanf("%d %d %d", &ageP, &ageR, &ageM);
    start = createStudent("Petra", ageP);
    end = start;
    newStudptr = createStudent("Remi", ageR);
    end = append(end, newStudptr);
    newStudptr = createStudent("Mike", ageM);
    end = append(end, newStudptr);

    printf("%s is %d years old.\n", start->name, start->age);
    printf("%s is %d years old.\n", start->next->name, start->next->age);
    printf("%s is %d years old.\n", start->next->next->name, start->next->next->age);

    tmp = start->next;
    free(start);
    start = tmp;
    tmp = start->next;
    free(start);
    free(tmp);

    return 0;
}

/* Place your function definitions here. Be sure to include the definition for 
   createStudent() and any other functions you created for the previous task. */
struct student *append(struct student * end, struct student * newStudptr) {
    //! heap=showMemory(start=260, cursors=[end,newDigitptr])
    end->next = newStudptr;
    //end = newStudptr;
    return(end->next);
}

struct student *createStudent(char studentName[], int studentAge) {
    struct student *ptr;
    ptr = (struct student *) malloc(sizeof(struct student));
    copyStr(studentName, ptr->name);  
    ptr->age = studentAge;
    ptr->next = NULL;
    return ptr;
}

void copyStr(char *source, char *target) {
    int i = 0;
    while (source[i]!='\0') {
        target[i] = source[i];
        i++;
    }
    target[i] = '\0';
}
```



struct student \*append还可以这样写：

```c
struct student *append(struct student * end, struct student * newStudptr) {
    //! heap=showMemory(start=260, cursors=[end,newDigitptr])
    end->next = newStudptr;
    end = newStudptr;
    return(end);
}
```

end->next = newStudptr是必不可少的，即使end后来赋值为newStudptr，原来的pionter也产生了意义。



# 3 Printing a linked list

## 3.1 Print a linked list

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit *next;
};

struct digit * createDigit(int);
struct digit * append(struct digit * end, struct digit * newDigptr);
void printNumber(struct digit *start);

int main(void) {
    //! stackk = showMemory(start=65520)
    struct digit *start, *newDigptr, *end, *tmp;
    int first = 5;
    int second = 3;
    int third = 7;
    start = createDigit(first);
    end = start;
    newDigptr = createDigit(second);
    end = append(end, newDigptr);
    newDigptr = createDigit(third);
    end = append(end, newDigptr);
    printNumber(start);
    tmp = start->next;
    free(start);
    start = tmp;
    tmp = start->next;
    free(start);
    free(tmp);
    return 0;
}

struct digit *createDigit(int dig) {
    struct digit *ptr;
    ptr = (struct digit *) malloc(sizeof(struct digit));
    ptr->num = dig;
    ptr->next = NULL;
    return ptr;
}

struct digit * append(struct digit * end, struct digit * newDigptr) {
    end->next = newDigptr;
    return(end->next);
}

void printNumber(struct digit *start){
    //! heap=showMemory(start=277, cursors=[ptr,start])
    struct digit * ptr = start;
    while (ptr!=NULL) {
        printf("%d", ptr->num);
        ptr = ptr->next;
    }
    printf("\n");
}
```



## 3.3 Activity: print a linked list of student data

In this task you will continue working on the linked list of students in which you would like to store, for each student,  their name and age. As before you are provided with some code that you  should not modify:

- A structure definition for the storage of each student's information.
- A main() function to test your code. 
- Prototypes for the functions createStudent(), append() (from previous tasks) and printStudents() (from the current task).

You will need the function definitions (from  previous tasks) for createStudent(), append() as well as any other  functions you added, such as copyStr() for example. If you were unable  to solve the previous task you have the option to be given the code for  the append() function (see the quiz preceding this task) so that you can work on the current task.

Your new task is to write a function printStudents() which takes as input a pointer that holds the address of the start of a linked list of students. Your function should then print this list of  students to the screen as specified in the example below. Your function  should not return anything.

### Provided code

 

```c
#include <stdio.h>
#include <stdlib.h>

struct student {
      char name[50];
      int age;
      struct student *next;
};

struct student *createStudent(char studentName[50], int studentAge);
struct student * append(struct student * end, struct student * newStudptr); 
void printStudents(struct student *start);
/* add other prototypes here if needed*/

int main(void) {
    struct student *start, *newStudptr, *end, *tmp;
    int ageP, ageR, ageM;

    scanf("%d %d %d", &ageP, &ageR, &ageM);

    start = createStudent("Petra", ageP);
    end = start;

    newStudptr = createStudent("Remi", ageR);
    end = append(end, newStudptr);

    newStudptr = createStudent("Mike", ageM);
    end = append(end, newStudptr);

    printStudents(start);
    tmp = start->next;

    free(start);

    start = tmp;
    tmp = start->next;

    free(start);
    free(tmp);

    return 0;
}

/* Place your function definitions here. Be sure to include the definitions for 
   createStudent() and append() as well as any other functions you created for 
   the previous tasks. */
```

### Example

#### Input: 

```
25 18 32
```

#### Output: 

```
Petra is 25 years old.
Remi is 18 years old.
Mike is 32 years old.
```