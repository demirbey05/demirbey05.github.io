+++
author = "Okan"
title = "Day 1 - Linkers Intro"
date = "2019-10-04"
description = "What is Linkers"
tags = [
    "100dosp",
]
+++


Programming tasks which is given us in college is generally in the form of single file, but what if we need to create a complex program such as browser. It is inefficient to create browser in a single file, so we need to divide the task into modules and files. After creating these files you need to merge into single executable. Linkers is needed at these stage. Linkers are the tools for merging a bunch of object files(a compiled version of a single .c or .cpp file) into a single executable object file.

Linking can be performed **at compile time, at load time, and even at run time**

Let's start with single example where we have two .c files : main.c and sum.c


```c
// main.c

int sum(int *a,int n); // function declaration must be in main,
// we can use .h files for this also

int array[2] = {1,2};

int main(){
    int val = sum(array,2);
    return val;
}

```
```c
// sum.c

int sum(int* a, int n){
    int i, s =0;

    for(i=0;i<n;i++){
        s+= a[i];
    }
    return s;
}
```

to create executable object file from these two code file we need to run at shell :
`linux> gcc -Og -o prog main.c sum.c`

After we wrote this command to shell, each file is processed by **preprocessor , compiler , assembler** to create **relocatable object file**. At the end we have two relocatable object file. `gcc` puts these two relocatable file to linker for getting a single executable `.prog`

By commanding `.prog` .The shell invokes a function in the operating system called the **loader**, which copies the code and data in the executable file prog into memory, and then transfers
control to the beginning of the program