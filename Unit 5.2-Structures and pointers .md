# 1 Create a structure to store the coordinates of a point

## 1.1  Create structures from user input

```c
#include <stdio.h>
struct point{
    int x;
    int y;
};
void printPoint(struct point pt);
void readPoint(struct point * ptr);
int main(void) {
    //! showMemory(start=65520)
    struct point z;
    readPoint(&z);
    printPoint(z);
	return 0;
}

void readPoint(struct point * ptr) {
    printf("\nEnter a new point: \n");
    printf("x-coordinate: ");
    scanf("%d", &ptr->x);
    printf("y-coordinate: ");
    scanf("%d", &ptr->y);
}

void printPoint(struct point pt){
    printf("(%d, %d)\n", pt.x, pt.y);
}
```



## 1.2 Use an array of structures

```c
#include <stdio.h>
struct point{
    int x;
    int y;
};
void printPoint(struct point pt);
void readPoint(struct point * ptr);
void printTriangle(struct point *ptr);
int main(void) {
    //! showMemory(start=65520)
    struct point triangle[3];
    int i;
    for (i=0; i<3; i++){
        readPoint(&triangle[i]);
    }
    printTriangle(triangle);
	return 0;
}

void readPoint(struct point * ptr) {
    printf("\nEnter a new point: \n");
    printf("x-coordinate: ");
    scanf("%d", &ptr->x);
    printf("y-coordinate: ");
    scanf("%d", &ptr->y);
}

void printTriangle(struct point *ptr) {
    int i;
    for (i=0; i<3; i++) {
        printPoint(ptr[i]);
    }
}

void printPoint(struct point pt){
    printf("(%d, %d)\n", pt.x, pt.y);
}
```



```printTriangle(triangle);```

而```void printTriangle(struct point *ptr);```，是因为array自带pointer信息，视为pointer；



我觉得```void printPoint(struct point pt);```中，不需要pt。



## 1.3 Activity: array of structures

第1题正确：

![image-20200406012842991](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200406012842991.png)



第2题错误：

![image-20200406012231657](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200406012231657.png)



正确答案是选：

第1个：pentagon[4].y = 4.1;

第5个：(pentagon+4)-&gt;y = 4.1;

网页markdown错误，图中的&gt，就是->



第6个错误原因，此处还的pentagon是pointer类型，不能直接指明y；猜测得用(*(pentagon+4).)y。



# 2 Allocate memory for structures

## 2.1 Allocate memory for structures

```c
#include <stdio.h>
#include <stdlib.h>
struct point{
    int x;
    int y;
};
void printPoint(struct point pt);
void readPoint(struct point * ptr);
void printPoly(struct point *ptr, int vertices);
int main(void) {
    //! showMemory(start=65520)
    struct point * polygon;
    int i, num;
    printf("How many vertices does your polygon have? ");
    scanf("%d", &num);
    polygon = (struct point *) malloc(num * sizeof(struct point));
    for (i=0; i<num; i++){
        readPoint(&polygon[i]);
    }
    printPoly(polygon, num);
    free(polygon);
	return 0;
}

void readPoint(struct point * ptr) {
    printf("\nEnter a new point: \n");
    printf("x-coordinate: ");
    scanf("%d", &ptr->x);
    printf("y-coordinate: ");
    scanf("%d", &ptr->y);
}

void printPoly(struct point *ptr, int vertices) {
    int i;
    for (i=0; i<vertices; i++) {
        printPoint(ptr[i]);
    }
}

void printPoint(struct point pt){
    printf("(%d, %d)\n", pt.x, pt.y);
}
```



# 2.2 Activity: allocate memory for structures

In this task, we will continue to work with polygons. You are provided with the following: 
\- A familiar structure definition for a 2-dimensional point.
\- Two familiar functions and their prototypes, "printPoint()" and "printPoly()".
\- A prototype for "initializePoly()", a function that you must write.
\- An empty main function which you must complete.

Please do not alter the provided code (except to fill in the main function and add your initializePoly() function).

initializePoly() should receive as input a pointer  to the first structure in an array of structures as well as in integer,  indicating how many points can be stored in the array. Your job is to  initialize these points in the following way: Using a for loop with i  starting at 0, initialize the x-coordinate of the point at index i as  -i, and the y-coordinate as i*i.

Your main function should read the number of  vertices to store in the array of points from the user, then allocate  the appropriate amount of memory, initialize the array with the function initializePoly, and finally print the vertices of the polygon using the function printPoly().

 

### Example

#### Input:

```
4
```

#### Output:

```
(0, 0)
(-1, 1)
(-2, 4)
(-3, 9)
```

 

### Provided code

```c
#include <stdio.h>
#include <stdlib.h>

struct point{
	int x;
	int y;
};

void printPoint(struct point);
void printPoly(struct point *, int);
void initializePoly(struct point *, int);

int main(void) {
    
    // Fill in your main function here

}

void printPoint(struct point pt) {
    printf("(%d, %d)\n", pt.x, pt.y);
}

void printPoly(struct point *ptr, int N) {
    int i;
    for (i=0; i<N; i++) {
        printPoint(ptr[i]);
    }
}

// Write your initializePoly() function here
```



我的程序：

```c
#include <stdio.h>
#include <stdlib.h>

struct point{
	int x;
	int y;
};

void printPoint(struct point);
void printPoly(struct point *, int);
void initializePoly(struct point *, int);

int main(void) {
    
    // Fill in your main function here
    struct point * ptr;
    int num;
    scanf("%d", &num);
    ptr = (struct point *) malloc(num * sizeof (struct point));
    initializePoly(ptr, num);
    printPoly(ptr, num);
    free(ptr);
    return 0;
}

void printPoint(struct point pt) {
    printf("(%d, %d)\n", pt.x, pt.y);
}

void printPoly(struct point *ptr, int N) {
    int i;
    for (i=0; i<N; i++) {
        printPoint(ptr[i]);
    }
}

// Write your initializePoly() function here
void initializePoly(struct point * ptr, int number){
    int i;
    for (i=0; i<number; i++){
        ptr[i].x = -i;
        ptr[i].y = i*i;
    }
}
```



# 3 Get to know the concept of a linked list

## 3.1 Link structures together in a linked list

```c
#include <stdio.h>

struct point{
    int x;
    int y;
    struct point * next;
};

int main(void) {
    //! showMemory(start=65520)
    struct point pt1 = {1, 2, NULL};
    struct point pt2 = {-2, 3, NULL};
    struct point pt3 = {5, -4, NULL};
    struct point * start, * ptr;
    
    start = &pt1;
    pt1.next = &pt2;
    pt2.next = &pt3;
    
    ptr = start;
    while (ptr!=NULL) {
        printf("(%d, %d)\n", ptr->x, ptr->y);
        ptr = ptr->next;
    }
	return 0;
}
```




## 3.2 Print a linked list

```c
#include <stdio.h>

struct point{
    int x;
    int y;
    struct point * next;
};
void printPoints(struct point *start);
int main(void) {
    //! showMemory(start=65520)
    struct point pt1 = {1, 2, NULL};
    struct point * start;
    struct point pt2 = {-2, 3, NULL};
    struct point pt3 = {5, -4, NULL};
    
    start = &pt1;
    pt1.next = &pt2;
    pt2.next = &pt3;
    
    printPoints(start);
    
	return 0;
}

void printPoints(struct point *start) {
    //! showMemory(start = 65520, cursors=[ptr])
    struct point * ptr;
    ptr = start;
    while (ptr!=NULL) {
        printf("(%d, %d)\n", ptr->x, ptr->y);
        ptr = ptr->next;
    }
}
```



## 3.3 Append new nodes to a linked list

```c
#include <stdio.h>

struct point{
    int x;
    int y;
    struct point * next;
};
void printPoints(struct point *start);
struct point * append (struct point * end, struct point * newpt);
int main(void) {
    //! showMemory(start=65520)
    struct point pt1 = {1, 2, NULL};
    struct point pt2 = {-2, 3, NULL};
    struct point pt3 = {5, -4, NULL};
    struct point * start, * end;
    
    start = end = &pt1;
    end = append(end, &pt2);
    end = append(end, &pt3);
    
    printPoints(start);
    
	return 0;
}

void printPoints(struct point *start) {
    //! showMemory(start = 65520, cursors=[ptr])
    struct point * ptr;
    ptr = start;
    while (ptr!=NULL) {
        printf("(%d, %d)\n", ptr->x, ptr->y);
        ptr = ptr->next;
    }
}

struct point * append (struct point * end, struct point * newpt) {
    end->next = newpt;
    return(end->next);
} 
```



## 3.4 Delete a linked list

```c
#include <stdio.h>
#include <stdlib.h>
struct point{
    int x;
    int y;
    struct point * next;
};
void printPoints(struct point *start);
struct point * createPoint(int x, int y) ;
struct point * append (struct point * end, struct point * newpt);
void freePoints(struct point * start);
int main(void) {
    //! showMemory(start=65520)
    struct point * start, * end, * newpt;
    int num, i;
    int x, y;
    
    printf("How many points? ");
    scanf("%d", &num);
    for (i=0; i<num; i++) {
        printf("x = ");
        scanf("%d", &x);
        printf("y = ");
        scanf("%d", &y);
        newpt = createPoint(x,y);
        if (i==0) {
            start = end = newpt;
        } else {
            end = append(end,newpt);
        }
    }
    printf("You entered: ");
    printPoints(start);
    freePoints(start);
	return 0;
}

void printPoints(struct point *start) {
    //! showMemory(start = 65520, cursors=[ptr])
    struct point * ptr;
    ptr = start;
    while (ptr!=NULL) {
        printf("(%d, %d)\n", ptr->x, ptr->y);
        ptr = ptr->next;
    }
}

struct point * append (struct point * end, struct point * newpt) {
    end->next = newpt;
    return(end->next);
} 

struct point * createPoint(int x, int y) {
    struct point *ptr;
    ptr = (struct point *)malloc(sizeof(struct point));
    ptr->x = x;
    ptr->y = y;
    ptr->next = NULL;
    return(ptr);
}

void freePoints(struct point * start) {
    struct point * ptr = start;
    while (ptr!=NULL) {
        start = ptr;
        ptr = ptr->next;
        free(start);
    }
}
```

