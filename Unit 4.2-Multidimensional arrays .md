# 1 Working with arrays and pointers

## 1.1 Define and work with arrays of pointers and use multiple ways for dereferencing

1. "\* arrays[0] = 5"，改变了a[0]的值；"* (arrays[0] + 1) = 6"，改变了a[1]的值

```c
#include <stdio.h>
int main(void){
     //! showMemory(cursors=[a, arrays[0], b, arrays[1], c, arrays[2]], start=65520)
    short a[3] = {234,655, 843};
    short b[2] = {12, 62};
    short c[4] = {3456, 3467, 23, 276};
    short * arrays[3] = {a, b, c};
    * arrays[0] = 5;
    * (arrays[0] + 1) = 6;
    * (arrays[0] + 2) = 7;
    return 0;
}
```



![image-20200402032336651](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200402032336651.png)



2. \* (arrays[0] + 1)等价于arrays[0][1]

```c
#include <stdio.h>
int main(void){
     //! showMemory(cursors=[a, arrays[0], b, arrays[1], c, arrays[2]], start=65520)
    short a[3] = {234,655, 843};
    short b[2] = {12, 62};
    short c[4] = {3456, 3467, 23, 276};
    short * arrays[3] = {a, b, c};
    * arrays[0] = 5; //a[0]
    arrays[0][0] = 0; //a[0]
    * (arrays[0] + 1) = 6; //a[1]
    arrays[0][1] = 0; //a[1]
    * (arrays[0] + 2) = 7; //a[2]
    arrays[0][2] = 0; //a[2]
    * arrays[1] = 3; //b[0]
    arrays[1][0] = 0; //b[0]
    * (arrays[1] + 1) = 4; //b[1]
    arrays[1][1] = 0; //b[1]
    return 0;
}
```

![image-20200402032854712](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200402032854712.png)



## 1.2 Use pointers to pointers and dereference

```c
#include <stdio.h>
void setToZero(short **);
int main(){
     //! showMemory(cursors=[t, t[0], t[1]],start=65520)
    short a[3] = {1245, 1924, 234};
    short b[2] = {24, 256};
    short * t[2] = {a,b};
    setToZero(t);
    return 0;
}
void setToZero(short ** t){
    *(*t) = 0; //t[0][0]  OR  *(t[0] + 0)
    *((*t) + 1) = 0;//t[0][1]  OR *(t[0] + 1)
    *((*t) + 2) = 0;//t[0][2]  OR *(t[0] + 2)
    *(*(t+1)) = 0;//t[1][0]  OR *(t[1] + 0)
    *(*(t+1)+1) = 0;//t[1][1]  OR *(t[1] + 1)
}
```



## 1.3 Activity: arrays and memory

You are designing a new cookie recipe and are  experimenting with different amounts of wet (water, oil) and dry (flour, sugar, cocoa powder) ingredients in order to get the proportions just  right. All of these amounts are initially read from the user input, and  the code to do so, along with all variable declarations, had already  been completed. You are interested in the total amount of wet and dry  ingredients used in the recipe as well as the ratio of these two  quantities.

Take a look at the code that is already given to  you. Your job is to add four lines of code, precisely where indicated by a comment such as

```
//Add one line here
```

Beneath each such line you will find an explanation  of what precisely your line of code is supposed to do as well as what  type of array addressing you are to use. Please read and follow these  directions carefully. Do not change anything else in the code that is  provided as our grading system will detect such changes and mark your  solution as incorrect.

### Example

#### Input

```
10.5 20.2                                                                                                                               
30.3 40.4 50.5
```

#### Output

```
Total amount of wet ingredients: 30.70 grams.                                                                                           
Total amount of dry ingredients: 121.20 grams.                                                                                          
Ratio of wet to dry ingredients: 3.95.                                                                                                  
New water amount: 15.35 grams, new oil amount: 15.35 grams. 
```

### Provided code

```c
#include <stdio.h>

int main(void) {

    double totalWet, totalDry, ratio;

    double wet[2];
    double dry[3];
    double * cookie[2] = {wet,dry};
    
    scanf("%lf%lf", &wet[0], &wet[1]);
    scanf("%lf%lf%lf", &dry[0], &dry[1], &dry[2]);

    // Add one line here! 
    /* The line you add should use the array cookie (and not the array wet) to 
       find the sum of the wet ingredients of the cookie recipe and store that sum
       in the variable totalWet. Use only indexed notation to address the cookie
       array (that is, you need to use two pairs of brackets [..]). 
    */

    printf("Total amount of wet ingredients: %.2lf grams.\n", totalWet);
    
    // Add one line here! 
    /* The line you add should use the array cookie (and not the array dry) to 
       find the sum of the dry ingredients of the cookie recipe and store that sum
       in the variable totalDry. This time, use only one pair of brackets [..] each 
       time you address the cookie array. 
    */

    printf("Total amount of dry ingredients: %.2lf grams.\n", totalDry);
    ratio = totalDry/totalWet;
    printf("Ratio of wet to dry ingredients: %.2lf.\n", ratio);

    // Add two lines here.
    /* The lines you add should use the array cookie (and not the array wet) to
       update the amounts of water and oil in your recipe. 
       You believe that any cookie recipe should use equal amounts of water and oil.
       Without changing the total amount of wet ingredients, update the values for
       water and oil, using only the array cookie (and not the array wet) so that 
       these amounts will be equal. The easiest way to do so is to assign the value
       totalWet/2 to both the water and the oil entry. When addressing the array cookie,
       do not use any brackets at all this time.
    */
    
    printf("New water amount: %.2lf grams, new oil amount: %.2lf grams.\n", wet[0], wet[1]);
    
    return 0;
}
```



我的程序：

```c
#include <stdio.h>

int main(void) {

    double totalWet, totalDry, ratio;

    double wet[2];
    double dry[3];
    double * cookie[2] = {wet,dry};
    
    scanf("%lf%lf", &wet[0], &wet[1]);
    scanf("%lf%lf%lf", &dry[0], &dry[1], &dry[2]);

    totalWet = cookie[0][0] + cookie[0][1]; // Add one line here! 
    /* The line you add should use the array cookie (and not the array wet) to 
       find the sum of the wet ingredients of the cookie recipe and store that sum
       in the variable totalWet. Use only indexed notation to address the cookie
       array (that is, you need to use two pairs of brackets [..]). 
    */

    printf("Total amount of wet ingredients: %.2lf grams.\n", totalWet);
    
    totalDry = *(cookie[1]) + *(cookie[1] + 1) + *(cookie[1] + 2); // Add one line here! 
    /* The line you add should use the array cookie (and not the array dry) to 
       find the sum of the dry ingredients of the cookie recipe and store that sum
       in the variable totalDry. This time, use only one pair of brackets [..] each 
       time you address the cookie array. 
    */

    printf("Total amount of dry ingredients: %.2lf grams.\n", totalDry);
    ratio = totalDry/totalWet;
    printf("Ratio of wet to dry ingredients: %.2lf.\n", ratio);

    wet[0] = (*(*cookie) + *(*cookie + 1))/2;
    wet[1] = wet[0];
    // Add two lines here.
    /* The lines you add should use the array cookie (and not the array wet) to
       update the amounts of water and oil in your recipe. 
       You believe that any cookie recipe should use equal amounts of water and oil.
       Without changing the total amount of wet ingredients, update the values for
       water and oil, using only the array cookie (and not the array wet) so that 
       these amounts will be equal. The easiest way to do so is to assign the value
       totalWet/2 to both the water and the oil entry. When addressing the array cookie,
       do not use any brackets at all this time.
    */
    
    printf("New water amount: %.2lf grams, new oil amount: %.2lf grams.\n", wet[0], wet[1]);
    
    return 0;
}
```



# 2 Storing and manipulating strings in arrays

## 2.1 Store strings in arrays using pointers

```c
#include <stdio.h>
int main(void){
     //! showMemory(cursors=[words[0], words[1], words[2]], start=65520)
    char a[4];
    char b[6];
    char c[9];
    char * words[3] = {a, b, c};
    printf("Please enter a word with at  most 3 letters: ");
    scanf("%s", a);
    printf("Please enter a word with at  most 5 letters: ");
    scanf("%s", b);
    printf("Please enter a word with at  most 8 letters: ");
    scanf("%s", c);
    printf("You entered: \n");
    printf("%s %s %s.\n", a, b, c);
    printf("%s %s %s.\n", words[0], words[1], words[2]);
    return 0;
}
```



"printf("%s %s %s.\n", a, b, c);"和”printf("%s %s %s.\n", words[0], words[1], words[2]);“的输出结果，相同。



## 2.2 Store multiple strings in an array

```c
#include <stdio.h>
int main(void){
    //! showMemory(cursors=[words[0], words[1], words[2]], start=65520)
    char words[3][10];
    int i;
    printf("Please enter three words: ");
    for (i=0; i<3; i++) {
        scanf("%s", words[i]);
    }
    printf("You entered: \n");
    for (i=0; i<3; i++) {
        printf("%s ", words[i]);
    }
    printf("\nFirst letters: \n");
    for (i=0; i<3; i++) {
        printf("\"%s\" starts with the letter '%c'.\n", words[i], words[i][0]);
    }
    return 0;
}
```



输出：

```
Please enter three words: Today is Monday.                                      
You entered:                                                                    
Today is Monday.                                                                
First letters:                                                                  
"Today" starts with the letter 'T'.                                             
"is" starts with the letter 'i'.                                                
"Monday." starts with the letter 'M'.  
```



## 2.3 Work with matrices

```c
#include <stdio.h>
int main(void){
    //! showMemory(cursors=[matrix[0], matrix[1]], start=65520)
    //! matrix = showArray2D(matrix, rowCursors=[line], colCursors=[col])
    int matrix[2][3];
    int line, col;
    for(line = 0; line < 2; line++){
        for(col = 0; col < 3; col++){
            scanf("%d",&matrix[line][col]);
        }
    }
    printf("You entered: \n");
    for(line = 0; line < 2; line++){
        for(col = 0; col < 3; col++){
            printf("%d ", matrix[line][col]);
        }
        printf("\n");
    }
   
    return 0;
}
```



输出：

```c
34 55 78                                                                        
-14 5 99                                                                        
You entered:                                                                    
34 55 78                                                                        
-14 5 99
```



## 2.4 Activity: print text in reverse order

Your goal is to  read a 68-word text from the input and then print it to the screen  backwards. Individual words do not have to be spelled backwards, but  rather your program should print out the last word first, then the  second-to-last word, etc. No word has more than 40 characters.

### Example

#### Input

Science Computer on Papers Selected Knuth, Ervin  Donald ― correct." be will results the that reader a convince to and  works algorithm an way the communicate to concepts, mathematical as well as forms literary and aesthetic traditional with works who essayist an  ideally is programmer A clearly. them understand can beings human that  so and quickly them perform can machines computing that so written are  programs best "The

#### Output

"The best programs are written so that computing  machines can perform them quickly and so that human beings can  understand them clearly. A programmer is ideally an essayist who works  with traditional aesthetic and literary forms as well as mathematical  concepts, to communicate the way an algorithm works and to convince a  reader that the results will be correct." ― Donald Ervin Knuth, Selected Papers on Computer Science



我的程序：

```c
#include <stdio.h>
int main(void){
    char matrix[68][40];
    int line;
    for(line = 0; line < 68; line++){
        scanf("%s", matrix[line]);
    }
    
    for(line = 67; line >= 0; line--){
        printf("%s ", matrix[line]);
    }
   
    return 0;
}
```