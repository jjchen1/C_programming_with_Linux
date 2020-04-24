[TOC]

# 1 Modularizing a program

## 1.1 GCC details

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra program.c -lm -o program
```



### 1.1.1 -std=c11

the -std=C11 tells the compiler which C standard to use.

The C standard we're using here is C11. That's a modern C standard.



### 1.1.2 -Wall

The -Wall means to display all warnings.

Sometimes the compiler registers a warning because it thinks you did something wrong, but it doesn't break the build command.

So in theory, you could still built the executable, but it's safe to always look at these warnings and try to fix them because typically, there's an error in your program.



### 1.1.3  -fmax-errors=10

Then this -fmax-errors here, that tells the compiler well, after 10 errors, stop, stop compiling and throwing more errors because I'll get overwhelmed.



### 1.1.4 -Wextra

And the -Wextra means extra warnings that are not included yet in the w all will also be displayed.



### 1.1.5 -o

I'm going type GCC minus O program that specifies the name of the output file.

Minus O stands for output file name so program is my executable.



### 1.1.6 ./program

program是program.c编译后的结果。

./program可以执行该程序。



### 1.1.7 如果没有指定output file name

let's simply type GCCprogram.C. Let's see what happened.

There was a file now called a.out.

That is actually my executable program.



### 1.1.8 C语言程序的执行过程

Now, let me show you what actually happens behind the scenes when you call GCC.

The first thing that happens is the preprocessor is called, which means it's a simple textual replacement. For example, the contents of scdio.h is found, which is a text file, and it's actually **verbatim copied into your source code**.

(There are other things that the preprocessor does, but we're not going to go into those details.)

Next, the source code is translated into machine language into a so-called **object file**. That object file in and of itself cannot be executed. But it is the binary computer readable version of your code.

And we can force that only that step happens by typing GCC. Again, we want to specify the output file name program.o, but now I want to stop at the object face program.c 

This is what we normally would have typed.

We now, in addition to that, give the compiler an option **-c**. This flag, **-c**, tells the compiler I only want to translate into machine language.

I do not yet want to create an executable program.

So when I run this GCC command, and now I type ls, there is a **program.o** and along with my program.c. But **I can't run that**.

You can see that because it didn't change color, but if I tried to run it, permission denied.

It doesn't work, and if I try to look at it, it is a bunch of gibberish. It is the **machine language version of my program**.



So GCC again.
I want to specify the name of my output file.

```
gcc -o program program.o
```



This time, I want to create my program.
And what I want to stick into GCC is program.o because I already have this object file.

And now, when I type ls, this executable program exists.

And when I run that, it does my average seven day temperature. So the compiler really does a number of things.

It calls the preprocessor, then it translates your code into** a language the computer can actually read**. And that is then taken by the linker, which **creates the executable program**.

So now you know how to separately compile and link your code into an executable program.

This is necessary in understanding how to split your source code up over multiple source files.

That's what we'll talk about next.



## 1.4 Object file

```
touch weatherstats.c
```



将program.c中的weatherstats相关内容，剪切给weatherstats.c。



```
gcc -c weatherstats.o weatherstats.c
```

生成weatherstats.o



但因为调用了weatherstats.h

```c
#include <weatherstats.h>
```



所以gcc语句也要有所表示：

```
gcc -o program program.o weatherstats.o
```



## 1.5 Activity : Linking

Here is where we left off after the previous video: We have three files, namely program.c, weatherstats.c and weatherstats.h.

```c
// program.c

#include <stdio.h>
#include "weatherstats.h"

int main(void) {
	double temperatures[7] = {6.9, 12.3, 9.0, 5.3, 9.8, 1.8, 0.3};
	double average = averageTemp(temperatures, 7);
	printf("Average 7-day temp: %.2lf\n", average);
	return 0;
}
// weatherstats.h:

double averageTemp(double *temps, int numOfTemps);
// weatherstats.c:

double averageTemp(double *temps, int numOfTemps) {
	double result = 0.0;
	int i;

	for (i=0; i<numOfTemps; i++) {
		result = result + temps[i];
	}

	result = result / (double) numOfTemps;
	return result;
}
```

You will need these files in Weblinux, so if you have not yet created and compiled them, please do so now.

Reminder:

compile program.c to program.o using

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c program.c -o program.o
```

compile weatherstats.c to weatherstats.o using

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c weatherstats.c -o weatherstats.o
```

link program.o and weatherstats.o into executable using

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra weatherstats.o program.o -o program
```

Create a new file myNewProgram.c with the following C-code:

```c
// myNewProgram.c

#include <stdio.h>
#include "weatherstats.h"

int main(void) {
    int N = 10;

    double temperatures[] = {60, 71.5, 88, 55.5, 49, 33.5, 32, 44.5, 49.0, 50};
    double average = averageTemp(temperatures, N);
    printf("Average %d-day temp: %.2lf\n", N, average);

    return 0;
}
```

Compile myNewProgram.c into an object file myNewProgram.o using

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c myNewProgram.c -o myNewProgram.o
```

Now try the following incorrect link command:

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra myNewProgram.o program.o -o myNewProgram
```



**习题：**

（在macbook上运行即可，WebLinux有问题。）

1. Copy and paste the second line of the long error message you receive (this line starts program.c: ) into the textbox below. Do not add any spaces before or after the text.

```

```

（未完成，因为用的不是WebLinux。下面已找到正确做法，这个错误信息无伤大雅。）



2. Now correctly link myNewProgram.o and weatherstats.o to an executable myNewProgram. How do you run myNewProgram? Type the commend to **run myNewProgram** in the textbox below.

```
./myNewProgram
```



3. What is the output you receive when running myNewProgram? **Copy the exact output you receive into the textbox below.** Do not add any spaces before or after the output.

```
Average 10-day temp: 53.30
```



## 1.7 Modify object files

```
gcc -Wall -c -o program.o program.c
gcc -Wall -c -o weatherstats.o weatherstats.c
gcc -Wall -o program program.o weatherstats.o
./program
```



输出：

```
Average 7-day temp: 6.49
Highest temp: 12.30
```



修改program的内容后，重新编译并执行（weatherstats.o不需要重新编译了）

```
gcc -Wall -c -o program.o program.c
gcc -Wall -o program program.o weatherstats.o
./program
```

输出：

```
Average 7-day temp: 7.91
Highest temp: 15.30
```



## 1.8 Activity: Super Image Project

You are teaching how to compile C programs and want to share your knowledge on creating and linking object files.

You have created a file with multiple functions to apply special effects to image files.

The source code for these functions is in a file named `image.c`. You want to create an object file from this file so that it can be used in multiple projects.

You then want to use these image functions in a "superimage" project  to show some examples! The source code of this example project is in `superimage.c` and the executable file is to be called `superimage`. 



**习题：**

1. What is the necessary compilation command to create an object file `image.o` from the source file `image.c`? Type your answer in the box below. Be sure to explicitely include the name of the output file using the -o option.

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c image.c -o image.o
```



2. What is the necessary compilation command to create an object file  superimage.o from the source file superimage.c? Type your answer in the  box below. Be sure to explicitely include the name of the output file using the -o option.

 ```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra -c superimage.c -o superimage.o
 ```



3. What is the necessary compilation command to link these object files together into your "superimage" project?

```
gcc -std=c11 -Wall -fmax-errors=10 -Wextra image.o superimage.o -o superimage
```



# 2 Creating and using a Makefile

## 2.1 Makefile

PROFESSOR: We will now see how to automate all of the necessary steps
to build the final executable program from source code spread out
over multiple files.
We will start with our previous program that
uses functions in the file weatherstats.c
to display the average as well as the highest temperature
from an array of temperatures.
Here on the left you see the program that we had written previously.
It has an array of temperatures, so type double and two variables
of type double, one named average and one named max.
And both of these variables are initialized by calling functions
from our weatherstats source file.
So with average, it's computed by calling the function
averageTemp, to which we pass the temperatures
array and the size of that array.
And max is initialized by calling MaxTemp
to which we also pass the temperatures array
as well as the size of that array.
And then simply, we print out the average seven-day temperature as well
as the highest temperature.
And that's it.
Just to quickly show you our weatherstats file only
contains these two functions, the average temperature function
and the max temperature function, which does exactly that.
And then the third file we have is the weatherstats.h file, which
contains the two headers.
So let me return to our program.
And there's nothing else in my directory.
I deleted everything else.
If I type LS here on the right hand side in the command prompt,
I see I only have program.c, weatherstats.c, and weatherstats.h.
I deleted all the object files in the executable.
So I cannot say run program right now because there is no such thing
as program.
Now the purpose of a make file is to automate
the building of executable programs.
We remember that it was kind of a nuisance.
We had to compile program.c into an object file program.o.
Then we had to separately compile weatherstats.c into weatherstats.o.
And then we had to link those two together.
So there were really three steps involved.
And to have to type all these commands and the compiler flags
was kind of annoying.
I will now show you how to use the program Make--
it's called Make-- to do multiple things all at once.
It'll do all of these compiling and linking steps for you.
The program Make, which is a program that
comes as part of a Linux distribution, reads instructions
from a so-called Makefile And so we're going
to create such a file of instructions.
To do so, I need to first create the file.
I'll do that with a touch command.
And now I can find it in my file browser.
So here's my Make file.
I'll open that.
And currently it has nothing in it.
So now we need to put something in it.
A Makefile has a very specific structure.
And the name of the Makefile is also fixed.
You can't name it anything else.
Here's the fixed structure.
I will first write this in English and then I'll give you an example.
First always comes a target.
And I'll tell you what that is.
A target is what is to be produced.
Then a colon, and then what is needed to do so, then a new line, a tab--
very important, you can't put spaces there, it has to be a tab--
and how to produce what you want to produce.
So let's start right out of the gate.
How do we produce our executable named program?
So that's my target.
Put a colon there.
And then, what is needed to do so?
Well, in order to get the executable program,
I need to program.0 and weatherstats.o.
These two files, I can then link together to create my program.
And how do I link those together?
First, I need to push my tab key, not spaces.
And now comes the command on how to do so.
And because I don't want to type all the compiler flags and all that,
I'm going to copy that.
But we'll then go through it.
So the Built command is GCC, and then all these compiler flags.
My output file is program.
So that's why the minus o program here in the very end.
And the two files that I want to link together
are program.o and weatherstats.o.
And we're done with this line.
Now we need to also tell the Makefile well, how do you make program.o.
And what does it depend on?
Well, program.o depends on program.c as well as weatherstats.h.
It needs that h file.
Because pound sign includes that h file.
And how do I build it once I have it?
Again, I'm going to just copy that and then go through it with you.
And the compile command is GCC and all these flags
that I was always too lazy to type.
But now since I'm simply pasting them in here, I can just put them there.
Then a minus c flag, that's very important,
to tell the compiler we're not building an executable.
We're only translating into machine language.
And then the file program.c, which is our source code, and the name
of the output file, minus o program.o.
And how do I create weatherstats.o?
With a very similar way.
It's created from weatherstats.c.
And how is that done?
Again, I'm going to copy that in and then simply go through it with you.
So there's my GCC command, all the flags, the minus c flag.
And the source code is in weatherstats.c.
The output is called weatherstats.o.
And that's it.
So now I'm going to remove my explanation at the top
because the Make program wouldn't understand English.
And I have these three targets.
Program is my ultimate target.
And whatever it needs, program.o comes underneath.
So program.o and weatherstats.o.
And they're both defined on how they are to be made.
So I'm going to save this.

And I can now run the Make command.
And I'm going to do that.
I can do that simply by typing Make on the right
or by putting my Build command as simply Make.
So I'll show you this way fast.
So as soon as I hit Run It, the Make command
will start working which executes Make.
But I'm going to watch in the browser what's happening.
So first off all, program.o showed up, weatherstats.o showed up,
and program showed up.
So three new files showed up.
And here in my window on the right, my terminal window, program was executed.
It says the average seven-day temperature is 7.91
and the highest temperature is 15.3 degrees.
I could have accomplished the same thing by simply
typing Make here on the right.
So let me demonstrate that.
Let me remove program and also everything that has an extension .o.
So see, everything is gone again.
And if I simply type Make here at the command prompt,
the same thing happens as before.
And it even echoes the GCC commands that were executed.
So that's nice to see.
All three commands were executed.
First, the commands to produce program.o was executed.
Then the command to produce weatherstats.o.
And then finally, they were linked together.
Now let's see what happens if I make a little change to something.
So let's go to the weatherstats.c file and make a little change.
Let's suppose I also wanted a minimum temperature function here.
I'm going to copy the Maximum Temperature function
and call it Minimum Temperature.
And then the function itself, the function body
is pretty much the same, except I'm going to call it Minimum.
And I find the minimum by comparing in the opposite way
to how it compared to the maximum.
So this is Minimum.
And I'm returning the minimum here.
Let me save that.
And let me also quickly update my weatherstats.h file.
Because I now have a minimum temperature function that I'm adding in there.
So I need a new header with Min.
And there it is.
Save it.
And probably in my program, I want to call that function.
So I'm going to call it.
I'm going to copy this line printf at the lowest temperature is.
And instead of Max, I want to call the Min function.
I could do that by simply creating a new variable named Min in the same way
I created it before.
Or I can actually call Min Temp directly here.

Let's save that.
And now, rather than having to painfully compile each file by hand,
then link it, and all that, I can simply type Make again here
at the command line.
And all these three commands are executed again.
And now if I run my program, it also displays the lowest temperature.
Now suppose I'm going to only make a little change.
Instead of lowest temp, I'm going to say lowest temperature.
And that's the only change I make.
So I haven't really updated my weatherstats.c file.
And the Make command is actually so smart it realizes
that there's nothing to be done.
It doesn't have to re-translate weatherstats.c into weatherstats.o.
There's nothing to be changed.
So when I now type Make here at the command prompt,
it only re-translates program.c into program.o
and then runs the link command.
Because otherwise, nothing has changed.
Now if I type Make again without making any change, it tells me,
there's nothing to make.
The program is up to date.
There's absolutely no reason.
So Make automatically checks for dependencies
and what things have changed.
It only re-translates or re-links those files
that actually have to be re-translated.
So now you know about these very important Make files
that actually allow the automation of the build process of an executable
program.
I strongly recommend that you try this out on your own now
by creating your own Make file for a project.
You'll see that this will greatly simplify the build process.
You return now to play with your own Make file.