# 1 Using strings (arrays of characters)

## 1.1 Store, print and read strings as arrays of characters

输入字符时，变量前不加&

scanf("%s", word);

```c
#include <stdio.h>
int main(void) {
    //! showArray(word, cursors[i])
    char word[51]; //arrray of characters (string)
    printf("Please enter a word with 50 letters: ");
    scanf("%s", word);
    printf("The word read is: %s.\n", word);
    printf("The characters are: <%c> <%c> <%c> <%c>\n", word[0], word[1], word[2], word[3]);
    word[1] = 'a';
    printf("The new word is %s\n", word);
    return 0;
}
```



## 1.2 Activity: repeat a word read from the user input

Write a C-program that prints out a word as many  times as specified. The number of repetitions and the word should be  given as input to the program. You may assume that the word has no more  than 100 characters (be sure to also reserve space for the null  terminator, \0, though!).

### Examples

#### Input:

```
2 Hello
```

#### Output:

```
Hello
Hello
```

 

#### Input:

```
4 thing
```

#### Output:

```
thing
thing
thing
thing
```



Hint 1 :

Use a for loop to repeat printing the scanned word as many times as necessary.



我的程序：

这样只能得85分，提示：“It looks like you did not declare an array of the correct size.
Make sure to add room for the null terminator, and don't use more space than you need to! (-15 points)”

```c
#include <stdio.h>
int main(void){
    int number, i;
    char word[100];
    scanf("%d %s", &number, word);
    for (i=0; i<number; i++){
        printf("%s\n", word);
    }

    return 0;
}
```



优化后，100分：因为数值算1位；空格算分隔符，不算1位。

```c
#include <stdio.h>
int main(void){
    int number, i;
    char word[101];
    scanf("%d %s", &number, word);
    for (i=0; i<number; i++){
        printf("%s\n", word);
    }

    return 0;
}
```



# 2 Using the special null terminator (\0) to identify the end of a string

## 2.1 Explain the null terminator \0

```c
#include <stdio.h>
int main(void) {
    //! word1 = showArray(word1, cursors=[i], width=0.5)
    //! word2 = showArray(word2, cursors=[i], width=0.5)
    char word1[5];
    char word2[8];
    scanf("%s %s", word1, word2);
    word1[3] = '\0';
    word2[2] = '\0';
    printf("%s %s\n", word1, word2);
    return 0;
}
```



## 2.2 Activity: swap first and last name

Your local public library keeps a record of all of  its patrons, consisting of index cards that hold a person's last name  followed by their first name (so that the cards can easily be sorted  alphabetically by last name). Unfortunately a computer error led to  incorrectly printed forms last month, resulting in a number of cards  that list the patron's first name followed by their last name rather  than the other way around. Your job is to read these pairs of first and  last names and display them in the correct order (last name followed by  first name). You may assume that each first and last name has at most  100 characters and does not contain any spaces.

Your program should first read the total number of  names (an integer) in order to know how many index cards need to be  processed altogether. Next, for each index card, your program should  read a patron's first name and last name and then display these names  correctly, that is on one line, the last name followed by one space,  followed by the first name. Your program should print the reversed name immediately after reading the patron's names (ie, it should not wait  until it has read all of the index cards to begin printing). 

Note that, for ease of viewing, the example below  shows all of the inputs in one block and all of the outputs in another  block, despite the fact that programmatically these will be  interspersed. 

### Example

#### Input:

```
4
Alan Turing
Ada Lovelace
Donald Knuth
Claude Shannon
```

 

#### Output:

```
Turing Alan
Lovelace Ada
Knuth Donald
Shannon Claude
```



我的程序：

```c
#include <stdio.h>
int main(void){
    int number, i;
    char firstName[10], lastName[10];
    scanf("%d", &number);
    
    for (i=0; i<number; i++){
        scanf("%s %s", firstName, lastName);
        printf("%s %s\n", lastName, firstName);
    }

    return 0;
}
```



# 3 Finding the length of a string

## 3.1 Find the length of a string

```c
#include <stdio.h>
int main(void) {
    //! showArray(word, cursors=[i])
    char word[30];
    int i = 0;
    printf("Please enter a word: ");
    scanf("%s", word);
    while (word[i]!='\0') 
        i++;
    printf("%s has word length %d.\n", word, i);
    return 0;
}
```



## 3.2 Activity: even or odd number of letters in a word?

At the annual meeting of MOOC fans, participants  register on the first day of the event in order to receive their name  tags, brochures and banquet vouchers. Unfortunately this often results  in long lines. In an attempt to speed things up, there are now two  people working the registration desk: one person who has the  registration materials for those fans whose names contain an odd number  of letters, the other for those whose names have an even number of  letters. Your job is to write a C-program that will tell a fan which  line to stand in.

To simplify the program, you may assume that student names are less than 50 characters long and contain no spaces. Your  program should output an integer value (1 or 2) depending on whether the fan should join line 1 (name has even number of letters) or line 2  (name has odd number of letters).

### Examples

#### Input:

```
Sharrock
```

#### Output:

```
1
```

 

#### Input:

```
Bonfert
```

#### Output:

```
2
```



我的程序：

```c
#include <stdio.h>
int main(void){
    char name[50];
    int i=0;
    scanf("%s", name);
    
    while (name[i] != '\0'){
        i++;
    }
    
    if (i%2 ==0){
        printf("1");
    } else {
        printf("2");
    }

    return 0;
}
```



# 4 Working with string lengths

## 4.1 Find the frequencies of word lengths

```c
#include <stdio.h>
int main(void) {
    //! showArray(word, cursors=[t])
    //! showArray(length, cursors=[i])
    int i = 0;
    int t = 0;
    int l = 0;
    int j = 0;
    int nbWords = 0;
    char word[11];
    int length[10];//length[5] number of 5-letter-long words in the text
    for(i=0;i<10;i++){
        length[i]=0;
    }
    scanf("%d", &nbWords);
    for(t=0;t<nbWords;t++){
        scanf("%s", word);
        l = 0;
        while(word[l]!='\0'){
            l++;
        }
        length[l] = length[l] + 1;
        printf("%s %d ", word,l);
    }
    for(j=0;j<10;j++){
        printf("There are %d words with %d letters.\n", length[j], j);
    }
    return 0;   
}
```



## 4.2 Activity: find the longest word in a text

Your job is to find the length of the longest word  in a text with no punctuation or special characters of any kind - only  contains words. To do so, please write a C-program that takes as a input first the number of words in a text, followed by all of the words in  the text. The output of your program should be the length of the longest word in the text.

To simplify your program, you can assume that the longest word will not exceed 100 characters.

### Examples

#### Input:

```
14
This is a simple example text
we have to find the largest word length
```

#### Output:

```
7
```

#### Input:

```
7
All cats are grey in the dark
```

#### Output:

```
4
```



我的程序：

```c
#include <stdio.h>
int main(void){
    char word[100];
    int number, i, l;
    int lMax=0;
    scanf("%d", &number);
    
    for (i=0; i<number; i++){
        scanf("%s", word);
        l = 0;
        while (word[l] != '\0'){
            l++;
        }
        if (l>lMax){
            lMax = l;
        }
    }
    
    printf("%d", lMax);
    return 0;
}
```



# 5 Sorting strings

## 5.1 Sort strings alphabetically

```c
#include <stdio.h>
int main(void) {
    char word1[50];
    char word2[50];
    int i = 0;
    
    printf("Please enter a word: ");
    scanf("%s", word1);
    printf("And another: ");
    scanf("%s", word2);
    // Find first letter in which words differ
    while (word1[i]!='\0' && word2[i]!= '\0' && word1[i] == word2[i]) 
        i++;
    if (word1[i] < word2[i])
        printf("%s comes before %s in the alphabet.\n", word1, word2);
    else if (word1[i]>word2[i])
        printf("%s comes after %s in the alphabet.\n", word1, word2);
    else printf("You entered the same word, %s, twice.\n", word1);
        
    return 0;
}
```



## 5.2 Search for a number in an array using linear search



## 5.3 Activity: is there a 't' in this word?

You are conducting a linguistic study and are  interested in finding words that contain the letter 't' or 'T' in the  first half of the word (including the middle letter if there is one).  Specifically, if the first half of the word does contain a 't' or a 'T', your program should output a 1. If the first half does not contain the  letter 't' or 'T', but the second half does, then your program should  output a 2. Otherwise, if there is no 't' or 'T' in the word at all,  your program's output should be -1. You may assume that the word entered does not have more than 50 letters.

 

### Examples

#### Input:

```
apple
```

#### Output:

```
-1
```

 

#### Input:

```
raincoat
```

#### Output:

```
2
```

 

#### Input:

```
enter
```

#### Output:

```
1
```

 

#### Input:

```
Taylor
```

#### Output:

```
1
```



我的程序：

```c

```