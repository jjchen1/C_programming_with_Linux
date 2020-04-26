[TOC]

# 1 Using arguments for main()

## 1.1 Pass arguments to a program from the command line

### 1.1.1 程序

```c
#include <stdio.h>

int main(int argc, char *argv[]){
  int i;
  printf("I have %d arguments from the command line: \n", argc);
  for (i=0; i<argc; i++){
    printf("Argument %d: %s\n", i, argv[i]);
  }
  
  return 0;
}
```



### 1.1.2 argv的3种表示

```int main(int argc, char *argv[]){```
可以2个\*号，去掉[]：```int main(int argc, char ** argv){```，
还可以2个[]：```int main(int argc, char argv[][]){```。

Because argv is a matrix. It's **an array containing pointers to an array of character**. So it's a matrix like this. 

So let's write it with double star, for example, **char \*\* **. It means that **argv** contains **an address to an array**, and **this array will contain**, in each cell, **a pointer to an array of character**.



### 1.1.3 argc

argc，是变量的数目，如下文

```
~ $ ./program -e -t
```

给出了2个变量：-e和-t。

而argc始终要在给出的变量数上+1。因为程序的名字，就是一个默认的变量。此处argc=3。



### 1.1.4 执行程序

```
~ $ ./program -e -t
I have %d arguments from the command line:
Argument 0: ./program
Argument 1: -e
Argument 2: -t
```



```
~ $ ./program first second third
I have 4 arguments from the command line: 
Argument 0: ./program
Argument 1: first
Argument 2: second
Argument 3: third
```



## 1.2 Use arguments passed to a program from the command line

### 1.2.1 将argument转换成对应的整数和小数

```
~ $ ./program -e 43 27.88
```

看起来，-e是string，43是整数，27.88是小数。

但实际上，上一节已经讲过，这些参数是char或string的array。



接下来的目标，就是将包含字符4和字符3的string，转换为整数43；将包含字符2、7、.、8、8的string，转化为数字27.88



### 1.2.2 程序

```c
#include <stdio.h>
#include <stdlib.h> //for atoi and atof
#include <string.h> //for strcmp

int main(int argc, char *argv[]){
  int i,  compare, wholeNumber;
  double decimalNumber;
  
  printf("I have %d arguments from the command line: \n", argc);
  for (i=0; i<argc; i++){
    printf("Argument %d: %s\n", i, argv[i]);
  }
  
  if (argc == 4){
    compare = strcmp(argv[i], "-e");
    if (compare ==0){
      printf("argv[1] equals -e \n");
    } else {
      printf("argv[1] does not equal -e \n");
    }
    wholeNumber = atoi(argv[2]);
    printf("%s is an integer is %d. \n", argv[2], wholeNumber);
    decimalNumber = atof(argv[3]);
    printf("%s is a double is %lf. \n", argv[3], decimalNumber);
  }
  
  return 0;
}
```



### 1.2.3 argv[1]，strcmp

从第15行开始

strcmp, stands for "string compare". it is defined in the string library string.h, therefore, is included here: ```#include <string.h>```. 如果2个string相同，将会返回值0。



### 1.2.4 argv[2]，atoi

argv[2]是一个string，包含2个character：4和3。

想要将其转换为integer，需要函数。函数atoi，可以实现ASCLL to integer。

atoi存在于标准library中，所以```#include <stdlib.h>```



### 1.2.4 argv[3]，atof

同理，用atof实现ASCLL to float，此处，将float，存于double变量decimalNumber中



### 1.2.5 运行程序

```
~ $ gcc program.c -o program
~ $ ./program -e 43 27.88
I have 4 arguments from the command line: 
Argument 0: ./cov
Argument 1: -e
Argument 2: 43
Argument 3: 27.88
argv[1] equals -e
argv[2] is an integer is 43.
argv[3] is a double is 27.88. 
```



## 1.3 Activity: pass numbers to a program from the command line

You are selling plants and are working on creating  invoices for customer orders. You are testing a program that should  receive, as arguments passed in from the command line, a number of  plants to be purchased (an integer) and the price per plant (a decimal  number). Your job is to create an invoice for the customer (see  examples) that prints out the total price of the order (which can be  found by multiplying the price per plant by the number of plants  purchased). 

If your program is called with an incorrect number  of arguments the user should receive the message "Invalid input" (see  Example 3).

Be sure to print prices with two decimal places, and to print the invoice exactly as presented in the examples below.

When testing your program in Weblinux, you need to  provide the command line arguments in the same way you just learned in  the video. When you submit your program to taskgrader however, we will  be supplying those arguments in order to test your program. In your  submission you thus do not have to worry about providing command line  arguments to your program.

**Examples**

**Input from the command line (via argv): **

```
5 2.39
```

**Output:**

```
5 plants for 2.39 dollars each cost 11.95 dollars.
```

 

**Input from the command line (via argv): **

```
2 48.99
```

**Output:**

```
2 plants for 48.99 dollars each cost 97.98 dollars.
```

 

**Input from the command line (via argv): **

```
48.99
```

**Output:**

```
Invalid input.
```



**我的程序：**

```c
#include <stdio.h>
#include <stdlib.h> //for atoi and atof

int main(int argc, char *argv[]){
  int number;
  double price;
  
  if (argc == 3){
    number = atoi(argv[1]);
    price = atof(argv[2]);
    printf("%d plants for %.2lf dollars each cost %.2lf dollars.", number, price, number*price);
  } else {
    printf("Invalid input.");
  }  
  
  return 0;
}
```



# 2 Reading from a file

## 2.1 Read numbers (integers and doubles) from a file using fscanf()

### 2.1.1 步骤123

1. open the file
2. read from the file
3. close the file



### 2.1.2 数据文件

my_first_file.txt

```
9
36 3 8 -11 8 -45 55 2 78
```

第一行的9，代表数据数量；第二行的9个数，代表具体数据。



### 2.1.3 主程序，读取数字9

program.c

```c
#include <stdio.>

int main(void){
  int N;
  FILE *ifile; /* ifile is a varible name - you could use any other name here. However, the '*' is important - we are working with a pointer. We call this a file pointer. */
  
  ifile = fopen("my_first_file.txt", "r"); /* open file for reading. The "r" stands for reading. */
  
  fscanf(ifile, "%d", &N); /* Read first name from the file. Just like scanf(), the only difference is the file pointer that gets passed in as well. */
  
  printf("There are %d numbers in the file.\n", N);
  
  fclose(ifile); /* closes the file */
  
  return 0;
}
```



6. r代表read，w代表write，a代表append。



8. fcanf和scanf的唯一区别，就是多了个参数，用来说明读取的文件是哪个。



### 2.1.4 修改程序，还要读取剩余数据

program.c

```c
#include <stdio.h>

int main(void){
  int N, i, number;
  FILE *ifile; /* ifile is a varible name - you could use any other name here. However, the '*' is important - we are working with a pointer. We call this a file pointer. */
  
  ifile = fopen("my_first_file.txt", "r"); /* open file for reading. The "r" stands for reading. */
  
  fscanf(ifile, "%d", &N); /* Read first name from the file. Just like scanf(), the only difference is the file pointer that gets passed in as well. */
  
  printf("There are %d numbers in the file.\n", N);
  
  for (i=0; i<N; i++){
    fscanf(ifile, "%d", &number);
    printf("I read %d from the file.\n", number);
  }
  
  fclose(ifile); /* closes the file */
  
  return 0;
}
```



## 2.2 Activity: read numbers from a file

You are teaching a class on C-programming! You would like to find out whether your teaching has been effective, and so you  need to compute the average grade your students have received on the  most recent assignment. These grades (integers) are stored in the file  studentGrades.txt.

The first entry in the file (an integer) is the  number of student grades that are stored in the file. For example, if  the file was as follows:

```
9
56 3 8 11 0 45 55 2 78
```

this would mean that there are 9 grades stored in the file (starting with 56 and ending with 78).

Your job is to calculate and print out the average  of the grades stored in the file. Please print the average grade with  two decimal places.

**Things to consider:**

To test your program you need to create your own  file "studentGrades.txt" with grades stored as described. In weblinux  you can do so by first typing "touch studentGrades.txt" at the command  prompt and then opening, editing and saving the file studentGrades.txt  in the file editor. When you submit your program to taskgrader we will  provide an input file for testing purposes. It is thus crucially  important that the file from which you are reading in your program is  indeed named "studentGrades.txt". 

**Examples**

**Input file "studentGrades.txt": **

```
4
100 99 90 98
```

**Output: **

```
96.75
```

 

**Input file "studentGrades.txt": **

```
2
100 50
```

**Output: **

```
75.00
```

 

**Input file "studentGrades.txt": **

```
7
90 88 76 93 44 98 33
```

**Output: **

```
74.57
```



**我的程序：**

```c
#include <stdio.h>

int main(void){
  int N, i;
  double sum=0;
  double number;
  
  FILE *ifile; 
  ifile = fopen("studentGrades.txt", "r"); 
  
  fscanf(ifile, "%d", &N);   
  for (i=0; i<N; i++){
    fscanf(ifile, "%lf", &number);
    sum += number;
  }  
  printf("%.2lf", sum/N);  
  fclose(ifile); /* closes the file */
  
  return 0;
}
```



# 3 Reading until the end of the file

## 3.1 Read until the end of the file

### 3.1.1 while循环

上一节，读取文本时，要先读取元素的数目。

这样操作比较麻烦，今天的课程用于解决这个问题。

program.c

```c
#include <stdio.h>

int main(void){
  int N, done, num, message;
  FILE *ifile; 
  
  ifile = fopen("my_first_file.txt", "r"); 
  done = 0;
  N = 0;
  
  while (!done) {
    message = fscanf(ifile, "%d", &num);    
    if (message == EOF){
      done = 1;
    } else {
      printf("I read %d from the file.\n", num);
      N++;
    }
  }
  
  printf("There are %d numbers in the file.\n", N);

  fclose(ifile); /* closes the file */
  
  return 0;
}
```



23. sum和N都是integer，所以前面需要加(douber)



### 3.1.2 求sum

```c
#include <stdio.h>

int main(void){
  int N, done, num, message, sum;
  FILE *ifile; 
  
  ifile = fopen("my_first_file.txt", "r"); 
  done = 0;
  N = 0;
  sum = 0;
  
  while (!done) {
    message = fscanf(ifile, "%d", &num);    
    if (message == EOF){
      done = 1;
    } else {
      printf("I read %d from the file.\n", num);
      N++;
      sum += num;
    }
  }
  
  printf("There are %d numbers in the file.\n", N);
  printf("The sum of the numbers read is %d.\n", sum);
  printf("The everage is %.2lf.\n", (double) sum/N);
  
  fclose(ifile); /* closes the file */
  
  return 0;
}
```



### 3.1.3 while循环太长了

将fscanf部分，放进while条件中

```c
#include <stdio.h>

int main(void){
  int N, num, sum;
  FILE *ifile; 
  
  ifile = fopen("my_first_file.txt", "r"); 
  N = 0;
  sum = 0;
  
  while (fscanf(ifile, "%d", &num) != EOF) {
    printf("I read %d from the file.\n", num);
    N++;
    sum += num;
  }
  
  printf("There are %d numbers in the file.\n", N);
  printf("The sum of the numbers read is %d.\n", sum);
  printf("The everage is %.2lf.\n", (double) sum/N);
  
  fclose(ifile); 
  
  return 0;
}
```



## 3.2 Activity: find the end of the file

You are still teaching a class on C-programming! You would like to find out whether the students in your class did better on the most recent assignment than the students in your colleagues'  classes. The average grades of all these classes are stored in a file  called "gradeComparison.txt". The first number stored in the file  represents the average grade of the students in your class. All of the  subsequent numbers represent the average grades of students from other  sections. For example, if the file contained the following:

```
95.23 94.80 91.56
```

this would mean that the students in your class  received an average grade of 95.23 on the last assignment, which is  higher than the average grades received by students in the other  sections.

If, on the other hand, the file was

```
95.23 94.80 91.56 96.40 93.25
```

then this would mean that the students in the fourth class received a slightly higher grade than the students in your class. 

Your job is to find out whether the students in your class did better than the students in the other classes and if so,  print out the word "Yes". If on the other hand students in another class did better than your students then you should print out "No", followed  by one space, followed by the number of the first class in the file that had a better grade average.

 

#### Things to consider: 

(1) Unlike in the previous task, this time the file  contains only average grades (and does not start with the number of  average grades stored in the file).

(2) To test your program you will need to create  your own file "gradeComparison.txt" with average grades stored as  described. In weblinux you can do so by first typing "touch  gradeComparison.txt" at the command prompt and then opening, editing,  and saving the file "gradeComparison.txt" in the file editor. When you  submit your program to taskgrader we will provide an input file for  testing purposes. It is thus crucially important that the file from  which you are reading in your program is indeed named  "gradeComparison.txt". 

**Examples**

**Input file "gradeComparison.txt": **

```
95.23 94.80 91.56
```

**Output: **

```
Yes
```

 

**Input file "gradeComparison.txt": **

```
95.23 94.80 91.56 96.40 93.25 99.64
```

**Output:**

```
No 4
```



**我的程序：**

```c
#include <stdio.h>

int main(void){
  double myGrade, grade;
  int N, isFirst;
  FILE *ifile; 
  
  ifile = fopen("gradeComparison.txt", "r"); 
  
  fscanf(ifile, "%lf", &myGrade);
  isFirst = 1;
  N = 1;
  
  while ((fscanf(ifile, "%lf", &grade) != EOF) && (isFirst == 1)) {
    N++;
    if (myGrade < grade){
      isFirst = 0;     
      printf("No %d", N);
    }
  }
  
  if (isFirst == 1){
    printf("Yes");
  } 
  
  fclose(ifile);
  
  return 0;
}
```



# 4 Writing to a file

## 4.1 Write numbers to a file using fprintf()

### 4.1.1 write numbers

```c
#include <stdio.h>

int main(void){
  int N = 10;
  FILE *ofile; /* ofile is a varible name - you could use any other name here. However, the '*' is important - we are working with a pointer. We call this a file pointer. */
  
  ofile = fopen("my_first_file.txt", "w"); /* open file for writing. The "w" stands for writing. */
  
  fprintf(ofile, "%d", N); /* Read first name from the file. Just like scanf(), the only difference is the file pointer that gets passed in as well. */
  
  
  fclose(ofile); /* closes the file */
  
  return 0;
}
```



my_first_file.txt的原内容被清空，写入了：10



### 4.1.2 do-while 循环写入

```c
#include <stdio.h>

int main(void){
  int N;
  FILE *ofile; 
  
  ofile = fopen("my_first_file.txt", "w"); 
  
  do {
    printf("Please enter a grade. Enter -1 to quit.\n");
    scanf("%d", &N); //不是fscanf 
    
    if (N != -1){
      fprintf(ofile, "%d ", N);//加上空格，防止写入文件时挤成一串
    }         
  } while (N != -1);
  
  fclose(ofile); 
  return 0;
}
```



**```fprintf(ofile, "%d ", N);```加上空格，防止写入文件时挤成一串**



### 4.1.3 用变量保存文件名

在fopen中写入文件名，不大方便；最好是在一开始，用变量定义文件名。

将```ofile = fopen("my_first_file.txt", "w"); ```改为

```
char filename[] = "my_first_file.txt";
ofile = fopen(filename, "w"); 
```



## 4.2 Append numbers to a file at the end

### 4.2.1 Append，将”w“改为”a“即可

```c
#include <stdio.h>

int main(void){
  int N;
  FILE *ofile; 
  
  char filename[] = "my_first_file.txt";
  ofile = fopen(filename, "r"); // a, means append
  
  do {
    printf("Please enter a grade. Enter -1 to quit.\n");
    scanf("%d", &N); //不是fscanf 
    
    if (N != -1){
      fprintf(ofile, "%d ", N);//加上空格，防止写入文件时挤成一串
    }         
  } while (N != -1);
  
  fclose(ofile); 
  return 0;
}
```

C语言很智能，如果一开始my_first_file.txt不存在，那么会直接新建my_first_file.txt文件



### 4.2.1 自主决定，是write还是append

先read文件，如果文件存在，就可以read；如果文件不存在，就可以得到系统传来的message。

```c
#include <stdio.h>

int main(void){
  int N;
  int selection = 1;
  FILE *ofile; 
  
  char filename[] = "my_first_file.txt";
  ofile = fopen(filename, "r");
  
  if (ofile != NULL){
    printf("You already have a file %s.\n", filename);
    fclose(ofile); //先把用read模式打开的file关闭，防止出错
    printf("Do you wich to (1) append or (2) overwrite it. Enter 1 or 2:\n");
    scanf("%d", &selection);
  }
  
  if (selection == 1){
    ofile = fopen(filename, "a");
  } else {
    ofile = fopen(filename, "w");
  }
  
  do {
    printf("Please enter a grade. Enter -1 to quit.\n");
    scanf("%d", &N); //不是fscanf 
    
    if (N != -1){
      fprintf(ofile, "%d ", N);
    }         
  } while (N != -1);
  
  fclose(ofile); 
  return 0;
}
```





## 4.3 Activity: write numbers to a file

You are grading final exams and you are recording  grades (integers) in a file "myGrades.txt". You just got distracted by a phone call and can't remember whether or not you already recorded the  grade of the student whose paper you just finished grading.

Expecting that this may not be the last time your  phone rings you decide to write a C-program to help you out. The program should first read, from the user input, the grade (an integer) that you need to check on. Next, the program should open the file  "myGrades.txt", find the last number in the file, close the file, and  compare the last number from the file to the grade read from the user  input. If the two grades are equal then you presumably already recorded  the grade and don't have to do anything. If on the other hand the two  grades do not equal each other then you have not yet recorded this new  grade and need to do so by appending this new grade to the file.

Finally, reopen the file and print its new contents to the screen.


**Things to consider:**

(1) Be sure to separate grades in the file by printing one space between the grades.

(2) To test your program you need to create your own file titled "myGrades.txt" with grades stored as described. In weblinux you can do so by first typing "touch myGrades.txt" at the command  prompt and then opening, editing and saving the file "myGrades.txt" in  the file editor. When you submit your program to taskgrader we will  provide an input file for testing purposes. It is thus crucially  important that the file from which you are reading in your program is  indeed named "myGrades.txt". 

(3) You may assume that you have already recorded  some grades in the file "myGrades.txt"; you therefore do not have to  check whether the file indeed exists (although you may, of course, do  so!)

 

**Examples**

**User input: **

```
83
```

**Input file "myGrades.txt": **

```
90 88 84 76
```

**File "myGrades.txt" after program terminates:**

```
90 88 84 76 83
```

 

**User input: **

```
76
```

**Input file "myGrades.txt": **

```
90 88 84 76
```

**File "myGrades.txt" after program terminates:**

```
90 88 84 76
```

**User input: **

```
88
```

**Input file "myGrades.txt": **

```
90 88 84 76
```

**File "myGrades.txt" after program terminates:**

```
90 88 84 76 88
```



**我的程序：**

```c
#include <stdio.h>

int main(void){
  FILE *ofile;
  int myGrade, grade, lastGrade;  
  char filename[] = "myGrades.txt";
    
  scanf("%d", &myGrade);
  
  ofile = fopen(filename, "r");  
  do {
    fscanf(ofile, "%d", &grade);
    lastGrade = grade;
  } while (fscanf(ofile, "%d", &grade) != EOF);  
  fclose(ofile); 
  
  if (lastGrade != myGrade){
     ofile = fopen(filename, "a");
     fprintf(ofile, " %d ", myGrade);
     fclose(ofile); 
  }
  
  ofile = fopen(filename, "r");
  while (fscanf(ofile, "%d", &grade) != EOF) {
    printf("%d ", grade);
  }  
  fclose(ofile); 

  return 0;
}
```