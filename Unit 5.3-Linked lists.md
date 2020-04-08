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



heap：是由malloc之类函数分配的空间所在地。地址是由低向高增长的。 
stack：是自动分配变量，以及函数调用的时候所使用的一些空间。地址是由高向低减少的。 

![image-20200409011746597](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409011746597.png)



回到main：

![image-20200409011816419](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409011816419.png)



free(numberptr)

![image-20200409011950139](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409011950139.png)



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



### 2.1.1 演示append

1. first生成start：

![image-20200409013011620](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409013011620.png)



2. stack中，start和end，陆续得到0x104

![image-20200409013220148](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409013220148.png)



3. 类似步骤，得到newdigit为0x110

![image-20200409013344350](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409013344350.png)



4. 进入append

![image-20200409014456203](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409014456203.png)



5. 完成“end->next = newDigitptr;”，地址01、10进入end->next

![image-20200409014904512](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409014904512.png)





6. 完成“end = newDigitptr;”，更新end的值为0110

![image-20200409015118227](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409015118227.png)



7. “return(end)”，将end的0110返回给，main中的end

![image-20200409015237066](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409015237066.png)



8. 重复步骤，完成third，则end有新的赋值0x11c：

![image-20200409015428831](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409015428831.png)



### 2.1.2 演示free

```c
    // free needs to be added  here
    tmp = start->next;
    free(start);
    start = tmp;
    tmp = start->next;
    free(start);
    free(tmp);
    return 0;
```

1. 完成“tmp = start->next;”，tmp=0x110

![image-20200409020157697](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409020157697.png)



2. 完成“free(start);”，free了0x104

![image-20200409020318601](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409020318601.png)



3. 完成“start = tmp;”， start=0x110

![image-20200409020412792](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409020412792.png)



4. 完成“tmp = start->next;”，tmp=0x11c

![image-20200409020445456](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409020445456.png)



5. 完成“free(start);”，free了0x110

![image-20200409020512037](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409020512037.png)



6. 完成”free(tmp);”，free了0x11c

![image-20200409020546791](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409020546791.png)



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



我的程序：

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
struct student *append(struct student * end, struct student * newStudptr) {
    //! heap=showMemory(start=260, cursors=[end,newDigitptr])
    end->next = newStudptr;
    return(end->next);
}

struct student *createStudent(char studentName[50], int studentAge) {
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

void printStudents(struct student *start){
    struct student * ptr = start;
    while (ptr!=NULL) {
        printf("%s is %d years old.\n", ptr->name, ptr->age);
        ptr = ptr->next;
    }
}
```



# 4 Free an entire linked list

## 4.1 Free all space allocated for a linked list

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit *next;
};

struct digit * createDigit(int);
struct digit * append(struct digit * end, struct digit * newDigptr);
void printNumber(struct digit *);
void freeNumber(struct digit *start);

int main(void) {
    //! stack = showMemory(start=65520)
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
    freeNumber(start);
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

void printNumber(struct digit *start) {
    struct digit * ptr = start;
    while (ptr!=NULL) {
        printf("%d", ptr->num);
        ptr = ptr->next;
    }
    printf("\n");
}

void freeNumber(struct digit *start) {
    //! heap=showMemory(start=277, cursors=[ptr,start,tmp])
    struct digit * ptr = start;
    struct digit * tmp;
    while (ptr!=NULL) {
        tmp = ptr->next;
        free(ptr);
        ptr = tmp;
    }
}
```



## 4.3 Activity: free a linked list of students

In this task you will continue working on the linked list of students in which you would like to store, for each student,  their name and age. As before you are provided with some code that you  should not modify:

- A structure definition for the storage of each student's information.
- A main() function to test your code. 
- Prototypes for the functions createStudent(), append(),  printStudents (from previous tasks) and freeStudents() (from the current task).

You will need the function definitions (from  previous tasks) for createStudent(), append(), printStudents() as well  as any other functions you added, such as copyStr() for example. If you  were unable to solve the previous task you have the option to be given  the code for the printStudents() function (see the quiz preceding this  task) so that you can work on the current task.

Your current task is to write a function  freeStudents() which takes as input a pointer that holds the address of  the start of a linked list of students. Your function should then free  the space allocated for each student in this list of students. Your  function should not return anything.

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
void printStudents(struct student *start);
void freeStudents(struct student *start);
/* add any other prototypes as needed */

int main(void) {
    struct student *start, *newStudptr, *end;
    int ageP, ageR, ageM;

    scanf("%d %d %d", &ageP, &ageR, &ageM);

    start = createStudent("Petra", ageP);
    end = start;
    newStudptr = createStudent("Remi", ageR);
    end = append(end, newStudptr);
    newStudptr = createStudent("Mike", ageM);
    end = append(end, newStudptr);

    printStudents(start);
    freeStudents(start);

    return 0;
}

/* Place your function definitions here. Be sure to include the definitions for 
   createStudent(), append(), printStudents() as well as any other functions you 
   created for the previous tasks. */
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
void printStudents(struct student *start);
void freeStudents(struct student *start);
/* add any other prototypes as needed */
void copyStr(char *source, char *target);

int main(void) {
    struct student *start, *newStudptr, *end;
    int ageP, ageR, ageM;

    scanf("%d %d %d", &ageP, &ageR, &ageM);

    start = createStudent("Petra", ageP);
    end = start;
    newStudptr = createStudent("Remi", ageR);
    end = append(end, newStudptr);
    newStudptr = createStudent("Mike", ageM);
    end = append(end, newStudptr);

    printStudents(start);
    freeStudents(start);

    return 0;
}

/* Place your function definitions here. Be sure to include the definitions for 
   createStudent(), append(), printStudents() as well as any other functions you 
   created for the previous tasks. */
struct student *append(struct student * end, struct student * newStudptr) {
    //! heap=showMemory(start=260, cursors=[end,newDigitptr])
    end->next = newStudptr;
    return(end->next);
}

struct student *createStudent(char studentName[50], int studentAge) {
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

void printStudents(struct student *start){
    struct student * ptr = start;
    while (ptr!=NULL) {
        printf("%s is %d years old.\n", ptr->name, ptr->age);
        ptr = ptr->next;
    }
}

void freeStudents(struct student *start){
    struct student * ptr = start;
    struct student * tmp;
    while (ptr != NULL){
        tmp = ptr->next;
        free(ptr);
        ptr = tmp;
    }
}
```



# 5 Creating linked lists from user input

## 5.1 Create a linked list of digits from user input

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit *next;
};

struct digit * createDigit(int);
struct digit * append(struct digit * end, struct digit * newDigptr);
void printNumber(struct digit *);
void freeNumber(struct digit *start);
struct digit * readNumber();

int main(void) {
    //! stack = showMemory(start=65520)
    struct digit *start;
    printf("Please enter a number: ");
    start = readNumber();
    printNumber(start);
    freeNumber(start);
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

void printNumber(struct digit *start) {
    struct digit * ptr = start;
    while (ptr!=NULL) {
        printf("%d", ptr->num);
        ptr = ptr->next;
    }
    printf("\n");
}

void freeNumber(struct digit *start) {
    struct digit * ptr = start;
    struct digit * tmp;
    while (ptr!=NULL) {
        tmp = ptr->next;
        free(ptr);
        ptr = tmp;
    }
}

struct digit * readNumber() {
    //! heap=showMemory(start=309, cursors=[start, end, newptr])
    char c;
    int d;
    struct digit *start, *end, *newptr;
    start = NULL;
    scanf("%c", &c);
    while (c!='\n') {
        d = c - 48;
        newptr = createDigit(d);
        if (start==NULL) {
            start = newptr;
            end = start;
        } else {
            end = append(end, newptr);
        }
        scanf("%c", &c);
    }
    return start;
}
```



输入：

```
Please enter a number: 735 
```



1. 输入7

readNumber()中，newptr地址为0127，end = start = newptr = 0x127，还有->next存在

![image-20200409023653487](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409023653487.png)



2. 输入3

newDigptr = 0x133

append()中，

end->next = newDigptr;，将0x133加入0x127对应的->next中



3. 输入5

newDigptr = 0x13F

append()中，

end->next = newDigptr;，

则0x133的->是 0x13F



## 5.2 Activity: check divisibility

In this task you will work with the linked list of  digits we have created in the lessons up to this point. As before you  are provided with some code that you should not modify:

- A structure definition for the storage of each digit's information.
- A main() function to test your code. 
- The functions createDigit(), append(), printNumber(), freeNumber() and readNumber() which we have written in the lectures.

Your task is to write a new function  divisibleByThree() which takes as input a pointer that holds the address of the start of a linked list of digits. Your function should then  check whether the number stored in this linked list of digits is  divisible by three. The function should return the value 1 if indeed the number is divisible by three and it should return the value 0  otherwise.

### Provided code

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit *next;
};

// Write your prototypes here

int main(void) {
    struct digit *start;
    start = readNumber();
    printf("The number ");
    printNumber(start);
    if (divisibleByThree(start)) 
        printf("is divisible by 3.\n");
    else
        printf("is not divisible by 3.\n");
    freeNumber(start);
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

void printNumber(struct digit *start) {
    struct digit * ptr = start;
    while (ptr!=NULL) {
        printf("%d", ptr->num);
        ptr = ptr->next;
    }
    printf("\n");
}

void freeNumber(struct digit *start) {
    struct digit * ptr = start;
    struct digit * tmp;
    while (ptr!=NULL) {
        tmp = ptr->next;
        free(ptr);
        ptr = tmp;
    }
}

struct digit *readNumber(void) {
    char c;
    int d;
    struct digit *start, *end, *newptr;
    start = NULL;
    scanf("%c", &c);
    while (c != '\n') {
        d = c-48;
        newptr = createDigit(d);
        if (start == NULL) {
            start = newptr;
            end = start;
        } else {
            end = append(end, newptr);
        }
        scanf("%c", &c);
    }
    return(start);
}

// Write your divisibleByThree() function here
```

### Examples

#### Input: 

```
234                                                                          
```

#### Output: 

```
The number 234
is divisible by 3.
```

#### Input: 

```
74658
```

#### Output: 

```
The number 74658
is divisible by 3.
```

#### Input: 

```
245
```

#### Output: 

```
The number 245
is not divisible by 3.
```



我的程序：

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit *next;
};

// Write your prototypes here
struct digit *createDigit(int dig);
struct digit * append(struct digit * end, struct digit * newDigptr);
void printNumber(struct digit *start);
void freeNumber(struct digit *start);
struct digit *readNumber(void);
int divisibleByThree(struct digit *start);

int main(void) {
    struct digit *start;
    start = readNumber();
    printf("The number ");
    printNumber(start);
    if (divisibleByThree(start)) 
        printf("is divisible by 3.\n");
    else
        printf("is not divisible by 3.\n");
    freeNumber(start);
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

void printNumber(struct digit *start) {
    struct digit * ptr = start;
    while (ptr!=NULL) {
        printf("%d", ptr->num);
        ptr = ptr->next;
    }
    printf("\n");
}

void freeNumber(struct digit *start) {
    struct digit * ptr = start;
    struct digit * tmp;
    while (ptr!=NULL) {
        tmp = ptr->next;
        free(ptr);
        ptr = tmp;
    }
}

struct digit *readNumber(void) {
    char c;
    int d;
    struct digit *start, *end, *newptr;
    start = NULL;
    scanf("%c", &c);
    while (c != '\n') {
        d = c-48;
        newptr = createDigit(d);
        if (start == NULL) {
            start = newptr;
            end = start;
        } else {
            end = append(end, newptr);
        }
        scanf("%c", &c);
    }
    return(start);
}

// Write your divisibleByThree() function here
int divisibleByThree(struct digit *start) {
    struct digit * ptr = start;
    int sum = 0;
    
    while (ptr!=NULL) {
        sum += ptr->num;
        ptr = ptr->next;
    }
    
    if (sum % 3 == 0){
         return 1;
    } else {
        return 0;
    }
}
```



# 6 Searching a linked list

## 6.1 Search for a node in a linked list

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit *next;
};

struct digit * createDigit(int);
struct digit * append(struct digit * end, struct digit * newDigptr);
void printNumber(struct digit *);
void freeNumber(struct digit *start);
struct digit * readNumber();
struct digit * searchNumber(struct digit * start, int number);

int main(void) {
    //! stack = showMemory(start=65520)
    struct digit *start, *ptr;
    int searchNum = 5;
    printf("Please enter a number: ");
    start = readNumber();
    printNumber(start);
    ptr = searchNumber(start, searchNum);
    if (ptr!=NULL) {
        printf("Found digit %d at location %p.\n", searchNum, ptr);
    } else {
        printf("Digit %d not found.\n", searchNum);
    }
    freeNumber(start);
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

void printNumber(struct digit *start) {
    struct digit * ptr = start;
    while (ptr!=NULL) {
        printf("%d", ptr->num);
        ptr = ptr->next;
    }
    printf("\n");
}

void freeNumber(struct digit *start) {
    struct digit * ptr = start;
    struct digit * tmp;
    while (ptr!=NULL) {
        tmp = ptr->next;
        free(ptr);
        ptr = tmp;
    }
}

struct digit * readNumber() {
    //! heap=showMemory(start=309, cursors=[start, end, newptr])
    char c;
    int d;
    struct digit *start, *end, *newptr;
    start = NULL;
    scanf("%c", &c);
    while (c!='\n') {
        d = c - 48;
        newptr = createDigit(d);
        if (start==NULL) {
            start = newptr;
            end = start;
        } else {
            end = append(end, newptr);
        }
        scanf("%c", &c);
    }
    return start;
}

struct digit * searchNumber(struct digit * start, int number) {
//! heap=showMemory(start=348, cursors=[ptr,start])
    struct digit * ptr = start;
    while ((ptr!=NULL) && (ptr->num!=number)) {
        ptr = ptr->next;
    }
    return(ptr);
}
```



## 6.2 Activity: update nodes in a linked list

In this task you will work with the linked list of  digits we have created in the lessons up to this point. As before you  are provided with some code that you should not modify:

- A structure definition for the storage of each digit's information.
- A main() function to test your code. 
- The functions createDigit(), append(), printNumber(), freeNumber(),  readNumber() and divisibleByThree() (although you may not need to use  all of these).

Your task is to write a new function changeThrees()  which takes as input a pointer that holds the address of the start of a  linked list of digits. Your function should change all of those digits  in this linked list that equal 3 to the digit 9, and count how many  replacements were made. The function should return this number of  replacements.

### Provided code

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit *next;
};

struct digit * createDigit(int dig);
struct digit * append(struct digit * end, struct digit * newDigptr);
void printNumber(struct digit *start);
void freeNumber(struct digit *start);
int divisibleByThree(struct digit * start);
struct digit * readNumber(void);
//Add your own function prototypes here

int main(void) {
    struct digit *start;
    start = readNumber();

    printf("The number ");
    printNumber(start);
    printf("was modified in %d places.\n", changeThrees(start));

    printf("The new number is ");
    printNumber(start);
    freeNumber(start);

    return 0;
}

struct digit * createDigit(int dig) {
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

void printNumber(struct digit *start) {
    struct digit * ptr = start;
    while (ptr!=NULL) {
        printf("%d", ptr->num);
        ptr = ptr->next;
    }
    printf("\n");
}

void freeNumber(struct digit *start) {
    struct digit * ptr = start;
    struct digit * tmp;
    while (ptr!=NULL) {
        tmp = ptr->next;
        free(ptr);
        ptr = tmp;
    }
}

struct digit * readNumber(void) {
    char c;
    int d;
    struct digit *start, *end, *newptr;
    start = NULL;
    scanf("%c", &c);
    while (c != '\n') {
        d = c-48;
        newptr = createDigit(d);
        if (start == NULL) {
            start = newptr;
            end = start;
        } else {
            end = append(end, newptr);
        }
        scanf("%c", &c);
    }
    return(start);
}

int divisibleByThree(struct digit * start) {
    struct digit * ptr = start;
    int qsum = 0;
    while (ptr!=NULL) {
        qsum += ptr->num;
        ptr = ptr->next;
    }
    if (qsum%3==0) return 1;
    else return 0;
}

// Write your changeThrees() function here
```

 

### Examples

#### Input: 

```
234345632                                                                       
```

#### Output: 

```
The number 234345632
was modified in 3 places.
The new number is 294945692
```

 

#### Input: 

```
4393293
```

#### Output: 

```
The number 4393293
was modified in 3 places.
The new number is 4999299 
```

 

#### Input: 

```
475692
```

#### Output: 

```
The number 475692
was modified in 0 places.
The new number is 475692
```



我的程序：

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit *next;
};

struct digit * createDigit(int dig);
struct digit * append(struct digit * end, struct digit * newDigptr);
void printNumber(struct digit *start);
void freeNumber(struct digit *start);
int divisibleByThree(struct digit * start);
struct digit * readNumber(void);
//Add your own function prototypes here
int changeThrees(struct digit * start);

int main(void) {
    struct digit *start;
    start = readNumber();

    printf("The number ");
    printNumber(start);
    printf("was modified in %d places.\n", changeThrees(start));

    printf("The new number is ");
    printNumber(start);
    freeNumber(start);

    return 0;
}

struct digit * createDigit(int dig) {
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

void printNumber(struct digit *start) {
    struct digit * ptr = start;
    while (ptr!=NULL) {
        printf("%d", ptr->num);
        ptr = ptr->next;
    }
    printf("\n");
}

void freeNumber(struct digit *start) {
    struct digit * ptr = start;
    struct digit * tmp;
    while (ptr!=NULL) {
        tmp = ptr->next;
        free(ptr);
        ptr = tmp;
    }
}

struct digit * readNumber(void) {
    char c;
    int d;
    struct digit *start, *end, *newptr;
    start = NULL;
    scanf("%c", &c);
    while (c != '\n') {
        d = c-48;
        newptr = createDigit(d);
        if (start == NULL) {
            start = newptr;
            end = start;
        } else {
            end = append(end, newptr);
        }
        scanf("%c", &c);
    }
    return(start);
}

int divisibleByThree(struct digit * start) {
    struct digit * ptr = start;
    int qsum = 0;
    while (ptr!=NULL) {
        qsum += ptr->num;
        ptr = ptr->next;
    }
    if (qsum%3==0) return 1;
    else return 0;
}

// Write your changeThrees() function here
int changeThrees(struct digit * start){
    struct digit * ptr = start;
    int num = 0;
    while (ptr!=NULL) {
        if (ptr->num == 3){
            ptr->num = 9;
            num +=1;
        }
        ptr = ptr->next;
    }
    
    return num;
}
```



# 7 Sorting a linked list using Insertion Sort

## 7.1 Insert a new node at the start of a linked list

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit *next;
};

struct digit * createDigit(int);
struct digit * append(struct digit * end, struct digit * newDigptr);
void printNumber(struct digit *);
void freeNumber(struct digit *start);
struct digit * readNumber();
struct digit * searchNumber(struct digit * start, int number);
struct digit * reverseNumber(struct digit * start);
struct digit * insertAtFront(struct digit * start, struct digit * newptr); 

int main(void) {
    //! stack = showMemory(start=65520)
    struct digit *start, *ptr, *backwards;
    printf("Please enter a number: ");
    start = readNumber();
    printNumber(start);
    backwards = reverseNumber(start);
    printNumber(backwards);
    freeNumber(start);
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

void printNumber(struct digit *start) {
    struct digit * ptr = start;
    while (ptr!=NULL) {
        printf("%d", ptr->num);
        ptr = ptr->next;
    }
    printf("\n");
}

void freeNumber(struct digit *start) {
    struct digit * ptr = start;
    struct digit * tmp;
    while (ptr!=NULL) {
        tmp = ptr->next;
        free(ptr);
        ptr = tmp;
    }
}

struct digit * readNumber() {
    char c;
    int d;
    struct digit *start, *end, *newptr;
    start = NULL;
    scanf("%c", &c);
    while (c!='\n') {
        d = c - 48;
        newptr = createDigit(d);
        if (start==NULL) {
            start = newptr;
            end = start;
        } else {
            end = append(end, newptr);
        }
        scanf("%c", &c);
    }
    return start;
}

struct digit * searchNumber(struct digit * start, int number) {
    //! heap=showMemory(start=348, cursors=[ptr,start])
    struct digit * ptr = start;
    while ((ptr!=NULL) && (ptr->num!=number)) {
        ptr = ptr->next;
    }
    return(ptr);
}

struct digit * insertAtFront(struct digit * start, struct digit * newptr) {
    //! heap=showMemory(start=348, cursors=[newptr,start])
    newptr->next = start;
    return(newptr);
}

struct digit * reverseNumber(struct digit * start) {
    //! heap=showMemory(start=336, cursors=[ptr,start,bstart,newdigit])
    struct digit *ptr = start;
    struct digit *bstart = NULL;
    struct digit *newdigit;
    
    if (start!=NULL) {
        bstart = createDigit(start->num);
        ptr = ptr->next;
    }
    while (ptr != NULL) {
        newdigit = createDigit(ptr->num);
        bstart = insertAtFront(bstart, newdigit);
        ptr = ptr->next;
    }
    return(bstart);
}
```



## 7.2 Create a sorted copy of a linked list

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit *next;
};

struct digit * createDigit(int);
struct digit * append(struct digit * end, struct digit * newDigptr);
void printNumber(struct digit *);
void freeNumber(struct digit *);
struct digit * readNumber(void); 
struct digit * searchNumber(struct digit * start, int number);
struct digit * insertAtFront(struct digit * start, struct digit * newptr);
struct digit * reverseNumber(struct digit * start);
struct digit * sortedCopy(struct digit * start);
struct digit * insertIntoSorted(struct digit *start, struct digit *newDig);

int main(void) {
    //! showMemory(start=65520)
    struct digit *start, *backwards, *sorted;
    printf("Please enter a number: ");
    start = readNumber();
    printf("You entered: ");
    printNumber(start);
    printf("Backwards: ");
    backwards = reverseNumber(start);
    printNumber(backwards);
    printf("Sorted by digit:");
    sorted = sortedCopy(start);
    printNumber(sorted);
    freeNumber(start);
    freeNumber(backwards);
    freeNumber(sorted);
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

void printNumber(struct digit *start) {
    struct digit * ptr = start;
    while (ptr!=NULL) {
        printf("%d", ptr->num);
        ptr = ptr->next;
    }
    printf("\n");
}

void freeNumber(struct digit *start) {
    struct digit * ptr = start;
    struct digit * tmp;
    while (ptr!=NULL) {
        tmp = ptr->next;
        free(ptr);
        ptr = tmp;
    }
}

struct digit * readNumber(void) {
    char c;
    int d;
    struct digit *start, *end, *newptr;
    start = NULL;
    scanf("%c", &c);
    while (c != '\n') {
        d = c-48;
        newptr = createDigit(d);
        if (start == NULL) {
            start = newptr;
            end = start;
        } else {
            end = append(end, newptr);
        }
        scanf("%c", &c);
    }
    return(start);
}

struct digit * searchNumber(struct digit * start, int number) {
    struct digit * ptr = start;
    while ((ptr!=NULL) && (ptr->num!=number)) {
        ptr = ptr->next;
    }
    return(ptr);
}

struct digit * insertAtFront(struct digit * start, struct digit * newptr) {
    newptr->next = start;
    return(newptr);
}

struct digit * reverseNumber(struct digit * start) {
    struct digit *ptr = start;
    struct digit *bstart = start;
    struct digit *newdigit;
    
    if (start!=NULL) {
        bstart = createDigit(start->num);
        ptr = ptr->next;
    }
    while (ptr != NULL) {
        newdigit = createDigit(ptr->num);
        bstart = insertAtFront(bstart, newdigit);
        ptr = ptr->next;
    }
    return(bstart);
}

struct digit * insertIntoSorted(struct digit *start, struct digit *newDig) {
    struct digit *ptr = start;
    struct digit *prev = NULL;
    while ((ptr!=NULL) && (ptr->num < newDig->num)) {
        prev = ptr;
        ptr = ptr->next;
    }
    if (prev == NULL) {
        start = insertAtFront(start, newDig);
    } else { //此处ptr==NULL，否则不会跳出上述while循环；prev等于start的最后一位字母，“prev->next = newDig;”，让prev末尾加入newDig；“newDig->next = ptr;”让newDig末尾为ptr，即使ptr等于NULL。
        prev->next = newDig;
        newDig->next = ptr;
    }
    return(start);
}

struct digit * sortedCopy(struct digit * start) {
    //! heap1=showMemory(start=348, cursors=[start, ptr, sortedStart, newDigit])
    //! heap2=showMemory(start=519, cursors=[start, newDigit, ptr, prev])
    struct digit *ptr = start;
    struct digit *sortedStart = NULL;
    struct digit *newDigit;
    
    if (start!=NULL) {
        sortedStart = createDigit(start->num);
        ptr = ptr->next;
    }
    while (ptr!=NULL) {
        newDigit = createDigit(ptr->num);
        sortedStart = insertIntoSorted(sortedStart, newDigit);
        ptr = ptr->next;
    }
    return(sortedStart);
}
```



输出：

```
Please enter a number: 764258947                                                
You entered: 764258947                                                          
Backwards: 749852467                                                            
Sorted by digit:244567789 
```



思路：

1. 完成sortedCopy()中struct的定义

![image-20200409025954366](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409025954366.png)



2. 完成语句```if (start!=NULL) {
    sortedStart = createDigit(start->num);
    ptr = ptr->next;
}```

sortedStart = 0x22a

ptr = 0x15e

![image-20200409030638522](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200409030638522.png)



3. 进入第1、2、3个while循环

完成```newDigit = createDigit(ptr->num);```，newDigit=0x236。

省略详情



4. 进入第4个while循环

完成```newDigit = createDigit(ptr->num);```，newDigit=0x25a。

进入insertIntoSorted()，

ptr = 0x24e, prev = 0x0



进入while ((ptr!=NULL) && (ptr->num < newDig->num)) 

第1次循环：2 < 5，prev = 0x24e（对应数值2），ptr = 0x242（对应数值4），newDig = 0x25a（对应数值5）

第2次循环：4 < 5， prev =  0x242（对应数值4），ptr = 0x236（对应数值6），newDig = 0x25a（对应数值5）



因为6>5，跳出while ((ptr!=NULL) && (ptr->num < newDig->num)) ，进入 if (prev == NULL) 的else分支：

“prev->next = newDig;”，则prev->next = 0x25a（对应数值5）；

“newDig->next = ptr;”，则newDig->next = ptr = 0x236（对应数值6）



于是，将5插进2467中，成为：24567。

分析完毕！



## 7.3 Activity: count redundancies in number

In this task you will again work with the linked list of digits we created during the lessons up to this point. 

You are provided with (but are not required to use)  the functions and prototypes we have written so far. You are also  provided with a main() function to test your code. Please do not modify  this main() function.

Your task is to write a new function countRedun()  which takes as input a pointer that holds the address of the start of a  linked list of digits. Your function should count how many redundancies  can be observed in the number stored in this list and return this count  of redundancies. A redundancy is a digit which has previously already  occurred in the number. For example, in the number 39534, the second '3' is a redundancy.

### Provided code

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit *next;
};


// Add a prototype for countRedun() here
struct digit * createDigit(int);
struct digit * append(struct digit * end, struct digit * newDigptr);
void printNumber(struct digit *);
void freeNumber(struct digit *);
struct digit *readNumber(void); 
int divisibleByThree(struct digit * start);
int changeThrees(struct digit * start);


// Do not modify this main() function
int main(void) {
    struct digit *start;
    start = readNumber();

    printf("The number ");
    printNumber(start);
    printf("contains %d redundancies.\n", countRedun(start));

    freeNumber(start);

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

void printNumber(struct digit *start) {
    struct digit * ptr = start;
    while (ptr!=NULL) {
        printf("%d", ptr->num);
        ptr = ptr->next;
    }
    printf("\n");
}

void freeNumber(struct digit *start) {
    struct digit * ptr = start;
    struct digit * tmp;
    while (ptr!=NULL) {
        tmp = ptr->next;
        free(ptr);
        ptr = tmp;
    }
}

struct digit *readNumber(void) {
    char c;
    int d;
    struct digit *start, *end, *newptr;
    start = NULL;
    scanf("%c", &c);
    while (c != '\n') {
        d = c-48;
        newptr = createDigit(d);
        if (start == NULL) {
            start = newptr;
            end = start;
        } else {
            end = append(end, newptr);
        }
        scanf("%c", &c);
    }
    return(start);
}

int divisibleByThree(struct digit * start) {
    struct digit * ptr = start;
    int qsum = 0;
    while (ptr!=NULL) {
        qsum += ptr->num;
        ptr = ptr->next;
    }
    if (qsum%3==0) return 1;
    else return 0;
}

int changeThrees(struct digit * start) {
    struct digit * ptr = start;
    int sum = 0;
    while (ptr!=NULL) {
        if (ptr->num == 3) {
            ptr->num = 9;
            sum++;
        }
        ptr = ptr->next;
    }
    return(sum);
}

// Write your countRedun() function here

```



### Examples

#### Input: 

```
5243
```

#### Output: 

```
The number 5243
contains 0 redundancies.
```

#### Input: 

```
5256202
```

#### Output: 

```
The number 5256202
contains 3 redundancies.
```

#### Input: 

```
7777
```

#### Output: 

```
The number 7777
contains 3 redundancies.
```



我的程序：

```c
#include <stdio.h>
#include <stdlib.h>

struct digit {
    int num;
    struct digit *next;
};

int countRedun(struct digit *start);
// Add a prototype for countRedun() here
struct digit * createDigit(int);
struct digit * append(struct digit * end, struct digit * newDigptr);
void printNumber(struct digit *);
void freeNumber(struct digit *);
struct digit *readNumber(void); 
int divisibleByThree(struct digit * start);
int changeThrees(struct digit * start);


// Do not modify this main() function
int main(void) {
    struct digit *start;
    start = readNumber();

    printf("The number ");
    printNumber(start);
    printf("contains %d redundancies.\n", countRedun(start));

    freeNumber(start);

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

void printNumber(struct digit *start) {
    struct digit * ptr = start;
    while (ptr!=NULL) {
        printf("%d", ptr->num);
        ptr = ptr->next;
    }
    printf("\n");
}

void freeNumber(struct digit *start) {
    struct digit * ptr = start;
    struct digit * tmp;
    while (ptr!=NULL) {
        tmp = ptr->next;
        free(ptr);
        ptr = tmp;
    }
}

struct digit *readNumber(void) {
    char c;
    int d;
    struct digit *start, *end, *newptr;
    start = NULL;
    scanf("%c", &c);
    while (c != '\n') {
        d = c-48;
        newptr = createDigit(d);
        if (start == NULL) {
            start = newptr;
            end = start;
        } else {
            end = append(end, newptr);
        }
        scanf("%c", &c);
    }
    return(start);
}

int divisibleByThree(struct digit * start) {
    struct digit * ptr = start;
    int qsum = 0;
    while (ptr!=NULL) {
        qsum += ptr->num;
        ptr = ptr->next;
    }
    if (qsum%3==0) return 1;
    else return 0;
}

int changeThrees(struct digit * start) {
    struct digit * ptr = start;
    int sum = 0;
    while (ptr!=NULL) {
        if (ptr->num == 3) {
            ptr->num = 9;
            sum++;
        }
        ptr = ptr->next;
    }
    return(sum);
}

// Write your countRedun() function here
int countRedun(struct digit *start){
    struct digit * ptr = start;
    int i, yesOrNo[10];
    int count = 0;
    
    for (i=0; i<10; i++){
        yesOrNo[i] = 0;
    }
    
    while (ptr != NULL){
        if (yesOrNo[ptr->num] == 1){
            count += 1;
        } else {
            yesOrNo[ptr->num] = 1;
        }
        ptr = ptr->next;
    }
    
    return count;
}
```