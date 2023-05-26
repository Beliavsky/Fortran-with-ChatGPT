# Fortran-with-ChatGPT
Questions about Fortran answered by ChatGPT

**Let's write a modern Fortran tutorial. Show a "Hello World" Fortran program with a comment line and explain how to compile and run the program on Linux and Windows.**

Absolutely, here is a simple Fortran "Hello World" program:

```
! This is a simple Fortran program
program HelloWorld
    implicit none
    print*, 'Hello, World!'
end program HelloWorld
```

Let's break down this code:

* `! This is a simple Fortran program` is a comment line in Fortran. Any line starting with ! is considered a comment and is not processed by the compiler.
* `program HelloWorld` starts the definition of a program called HelloWorld.
* `implicit none` is a statement that tells the Fortran compiler to require explicit declaration of all variables. It's considered good practice to include this in all your Fortran programs to avoid possible problems with undeclared variables or misspelled variable names.
* `print*, 'Hello, World!'` is a statement that prints "Hello, World!" to the console.
* `end program HelloWorld` ends the program definition.
