**Tell me about variables.**

In Fortran, as in many other programming languages, variables are used to store data that your program can manipulate. Each variable in Fortran has a name, a type, and a value.

Here are the main types of variables in Fortran:

1. **Integer**: This is used to store integer values. For example:
    ```Fortran
    integer :: x
    x = 5
    ```

2. **Real**: This is used to store real numbers (i.e., floating point values). For example:
    ```Fortran
    real :: y
    y = 3.14
    ```

3. **Complex**: This is used to store complex numbers. A complex number has a real part and an imaginary part. For example:
    ```Fortran
    complex :: z
    z = (1.0, 2.0)  ! 1.0 is the real part and 2.0 is the imaginary part
    ```

4. **Logical**: This is used to store logical values, i.e., `.true.` or `.false.`. For example:
    ```Fortran
    logical :: is_true
    is_true = .true.
    ```

5. **Character**: This is used to store characters or strings. For example:
    ```Fortran
    character(len=5) :: s
    s = "Hello"
    ```

Variable names in Fortran must start with a letter and can contain letters, digits, and underscores. The Fortran language is case insensitive, meaning that `myVariable`, `MYVARIABLE`, and `MyVariable` would all refer to the same variable.

Before using a variable in Fortran, it must be declared in a type declaration statement (as shown in the examples above). The `::` symbol is used to separate the variable type from the variable name(s) in the declaration. You can declare multiple variables of the same type on the same line by separating the names with commas, like so: `integer :: x, y, z`.

The `implicit none` statement is commonly used in Fortran programs to require that all variables be explicitly declared. If you don't include this statement, Fortran will implicitly declare variables according to rules based on the first letter of the variable name, which can sometimes lead to confusing bugs if you make a typo in a variable name.

You can also specify the precision of `real` and `complex` variables when you declare them. For example, `real(kind=8) :: x` declares `x` as a double-precision real variable. (**Note:** That is not guaranteed to work with all compilers. It is better to write define a kind parameter with something like `integer, parameter :: dp = kind(1.0d0)` and then write `real(kind=dp)`). The `kind` parameter determines the precision and range of the variable.

---
**What is a "double-precision" real variable?**

A "double-precision" real variable in Fortran is a type of floating-point variable that offers greater precision (i.e., more significant digits) and a wider range than "single-precision" real variables. The term "double-precision" comes from these variables utilizing twice the number of bits as single-precision variables.

In terms of bits, a single-precision real number usually uses 32 bits, while a double-precision real number uses 64 bits. The exact specifics can vary by system and compiler, but in general:

- Single-precision real variables can typically provide up to 7 decimal digits of precision, with a range of about 1.2E-38 to 3.4E+38.
- Double-precision real variables can provide up to 15 decimal digits of precision, with a range of about 2.2E-308 to 1.8E+308.

In Fortran, you can declare a double-precision variable with a statement like this:

```Fortran
double precision :: x
```

Or, you can use the `kind` specifier with the `real` type to declare a variable of a specific kind (precision). For instance, `kind=8` is commonly used for double-precision:

```Fortran
real(kind=8) :: x
```

(**Note:** see the comment above warning against declarations such as `real(kind=8)`). Remember that using more precise variables consumes more memory, so it's a good idea to use the level of precision that's appropriate for your needs.

---
**How do you display the values of variables you have set?**

You can display the values of variables in Fortran using the `print` or `write` statements.

Here's a simple example that demonstrates this with an integer, a real, a logical, and a character variable:

```Fortran
program DisplayValues
    implicit none
    integer :: x
    real :: y
    logical :: is_true
    character(len=10) :: s

    x = 5
    y = 3.14
    is_true = .true.
    s = "Hello"

    print*, 'The value of x is: ', x
    print*, 'The value of y is: ', y
    print*, 'The value of is_true is: ', is_true
    print*, 'The value of s is: ', s
end program DisplayValues
```

In this program, the `print` statement is used to display the values of the variables. The `*` in the `print` statement is a placeholder for the output format - in this case, we're using the default format. Following the `,` you can list any number of variables or strings to print. The variables and strings will be printed in the order you list them.

You could run this program, and it would display the values of the variables `x`, `y`, `is_true`, and `s`.

Also, please note that Fortran will print logical variables as `T` for `.true.` and `F` for `.false.`.

---
**What are the values of variables before they are set?**

In Fortran, as in many other programming languages, variables that are declared but not initialized can contain "garbage" values -- whatever data happened to be in the memory location assigned to the variable.

For example, consider the following Fortran code:

```Fortran
program UninitializedVar
    implicit none
    integer :: x
    print*, 'The value of x is: ', x
end program UninitializedVar
```

If you run this program, it may print out a random number as the value of `x`, or it might cause a runtime error, depending on the compiler and runtime environment. The value of `x` before it's initialized is unpredictable, so you should always initialize your variables before you use them.

Fortran provides a convenient way to declare and initialize a variable in one line. Here's an example:

```Fortran
program InitializedVar
    implicit none
    integer :: x = 10
    print*, 'The value of x is: ', x
end program InitializedVar
```

In this program, `x` is declared as an integer and initialized to `10`. If you run this program, it will consistently print `The value of x is:  10`, because `x` is initialized before it's used.
