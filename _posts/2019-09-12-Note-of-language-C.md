---
layout:     post
title:    "Note of language C from chapter 1 to 4"
subtitle:   "finished note"
date:     2019-09-12
author:     "rick"
header-img: "img/post-c-language.png"
tags:
- Study note
---

To learn language C and memerize some important points better, I decided to start a blog to keep some difficult and tricky points I met in the study of C.

### The compilation of c

Usually, in the terminal, we use the command

`gcc -Wall -std=c99 -o exefile_name .cfile_name`

to compile the language. 

Note: 

- There is no mid file .o because it uses -o the compile directly. 
- -Wall means shows all warnings after the compilation. 
- -std=c99 means the version of C is C99 which is an old version replaced by C11 in 2011.
- the positions of exefile_name and .cfile_name cannot be changed. Otherwise gcc will not find the input file.

<!--To be updated here: the theroy of the gcc compiler-->



We use /* ... */ to comment in C. e.g. : 

`/************************************************/`
`/* Converts a Fahrenheit temperature to Celsius */
/* *Name: celsius.c* */
/* *Author: K. N. King*/`
`/* *September 11, 2017 ***************************/`



#### Three standard I/O in <stdio.h> 

-- stdin (from keyboard to screen terminal)

-- stdout (terminal screen)

-- stderr (terminal screen, it will display the error)



The return value in the end of main is the status code which indicates that the program is already finished.

The use of define: # define a b (define b as a/use a to replace b) and this is macro definition



#### The use of % and &:



#### The identifiers in C:

start with a letter or underscore

case sensitive





#### printf:

In the case printf("%d %d", a);  a is an int, it will print a's value and print the meaningless content.

In the case printf("%d", a, b); it will only print the value of a.

We cannot use printf("%f", a); a is an int to change the type of the output since the output will become meaningless.



The  conversion specification in the printf

```c
#include <stdio.h>
int main(void) {
	int i;
	float x;
	i = 40;
	x = 839.21f;
	printf("|%d|%5d|%-5d|%5.3d|\n", i, i, i, i);
	printf("|%f|%10.3f|%10.3e|%-10g|\n", x, x, x, x);
	return 0;
}
```

Result:

```
|40| 40|40 | 040|
|839.210022|   839.210| 8.392e+02|839.21   |
```



#### difference between %f and %e:

%f display the decimal format, in the %.pf, p means 保留几位小数.

%e display the exponential format, same p's function.

%g display either exponential or decimal format, depending on the size of the number.



"%-5d" means 靠右对齐 and 显示五位,不足的用empty space 代替.

If we want to print ", we use \\", for example printf("\\"hello\\"") ; prints "hello".





#### scanf:

& in the scanf means the memory unit address of the variable, it pointing to the memory address.



The return value of scanf:

```c
#include <stdio.h>
#define FREEZING_PT 32.0f
#define SCALE_FACTOR (5.0f / 9.0f)
int main(void) {
	float fahrenheit, celsius;
	for (;;) {
		printf("Enter Fahrenheit temperature (non-number to quit): ");
		if (scanf("%f", &fahrenheit) == 1) f
			celsius = (fahrenheit - FREEZING_PT) * SCALE_FACTOR;
			printf("Celsius equivalent: %.1f\n", celsius);
		}
		else break;
	}
	return 0;
}
```

output:

```
Enter Fahrenheit temperature (non-number to quit): 8
Celsius equivalent: -13.3
Enter Fahrenheit temperature (non-number to quit): 0
Celsius equivalent: -17.8
Enter Fahrenheit temperature (non-number to quit): 1 2
Celsius equivalent: -17.2
Enter Fahrenheit temperature (non-number to quit): Celsius equivalent: -16.7
Enter Fahrenheit temperature (non-number to quit): p
```

The first two cases are normal. In the third case,  user input two numbers but scanf only has one place to store. so it displays the output in the next loop directly through the remaining input in the last function which is 2 in this case. In the last case, the return value of scanf is 0, so the if statement terminates the loop.



The input of several contents

```c
#include <stdio.h>
int main() {
    int i,j;
    float x, y;
    scanf("%d%d%f%f", &i, &j, &x, &y);
    printf("%d  %d  %f  %f",i,j,x,y);
    return 0;
}
```

result:

```
Input: 1 -20 .3 -4.0e3
ouput: 1  -20  0.300000  -4000.000000

input:1
n-20 
	.3
-4.0e3
output:1  -20  0.300000  -4000.000000

input: 1-20.3-4.0e3
output:1  -20  0.300000  -4000.000000
```

In the last case, after read in the number 1, scanf finds the - and - can not appear inside an number, so puts it back can store 1 in the variable i. After finding the second number -20, scanf finds ., and the . can not appear inside the number. By this kind of way, scanf successfully reads four numbers.



#### The format ieee 754 of binary:

Three parts of ieee 754:

- sign (1 bit)
- exponent (8 bits)
- fraction(23 bits)





#### Expression:

###### side effect in assignment:

when assigning int i = 72.99f;, Since the variable i is int, the .99 will be discarded directly. This is called the side effect of assignment. 

After computing the value, the variable i is also changed, this is side effect.

i += j += k is equal to i += (j+=k)



###### difference between i++ and ++i:

i++: use i first and plus one

++i: plus one first and then use i

```c
#include <stdio.h>
int main() {
    int i = 1;
    int a = 3;
    printf("%d\n", (i++) + a);
    i = 1;
    printf("%d\n", (++i)+a); 
    return 0;
}
```

result:

```
4
5
```

The lvalue(left value) in the assignment is an object stored in memory which cannot be a number or a character.

The expression can be a statement without lvalue but after it is calculated, it will be discarded. so it is useful only when side effect works on.



<!--code and output about input/output and expression:--> 







