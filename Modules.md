## Modules, Functions, and Subroutines

**Discuss the roles of modules, functions, and subroutines in Fortran.**

In Fortran, modules, functions, and subroutines are key elements of the language that serve different purposes and have distinct roles.

1. Modules:
   - Modules are used to encapsulate related variables, types, constants, and procedures (functions and subroutines) into a single unit.
   - Modules provide a way to organize and modularize code by grouping related entities together.
   - They allow for the separation of interface and implementation details, providing a clean and structured approach to program development.
   - Modules enable information sharing among different program units (such as functions and subroutines) by using the `use` statement to access the entities defined within the module.

2. Functions:
   - Functions are reusable program units that perform specific computations and return a value.
   - They are designed to accept input arguments, perform computations using those arguments, and return a result.
   - Functions can be used in expressions, assigned to variables, or passed as arguments to other procedures.
   - Functions are useful for performing calculations and returning results that can be used in different parts of a program.

3. Subroutines:
   - Subroutines are reusable program units that perform a series of instructions or actions without returning a value.
   - They can have input and output arguments but do not have a return value.
   - Subroutines are typically used for procedures that modify the values of input arguments or perform certain actions without needing to return a result.
   - Subroutines can be called from other parts of the program to perform specific tasks or operations.

In summary, modules are used for organizing and sharing related entities, functions are used for performing computations and returning results, and subroutines are used for executing a series of actions or modifying input arguments. Each of these elements plays a crucial role in structuring Fortran programs and promoting code reusability, modularity, and clarity.

---
**Why should you put functions and subroutines in modules?**

Putting functions and subroutines in modules offers several advantages in Fortran programming:

1. Encapsulation: Modules provide a way to encapsulate related functions and subroutines along with associated variables, types, and constants. This encapsulation promotes code organization and modular design, making it easier to understand and maintain the codebase. By grouping related procedures within a module, you create a logical unit that represents a specific functionality or component of your program.

2. Information Sharing: Modules allow for information sharing among different parts of a program. By placing functions and subroutines in modules, you can use the `use` statement to access and utilize the entities defined within the module from other program units. This promotes code reuse and avoids the need to redefine functions or subroutines in multiple places, enhancing code clarity and reducing redundancy.

3. Name Scope Management: Modules define their own name scopes, which helps avoid naming conflicts and promotes proper scoping of variables and procedures. By placing functions and subroutines within modules, you can avoid naming clashes with entities defined in other parts of the program.

**Note:** when a procedure is placed in a module and another program USEs the module to access the procedure, the compiler checks that the procedure is being called with appropriate arguments. Functions and subroutines being called with the wrong argument types was a common error in Fortran 77, which did not have modules.

---
**How do functions work?**

In Fortran, functions are subprograms that perform specific tasks and return a value to the calling program. They are defined using the `function` keyword and can take zero or more arguments as input. Functions are typically used to perform calculations or transformations on input values and produce a result.

Here's the general syntax for defining a function in Fortran:

```fortran
[attributes] function function_name(arg1, arg2, ...) result(return_value)
    [variable declarations]
    [executable statements]
end function function_name
```

Let's break down the different components of a function:

- `attributes` (optional): You can specify attributes such as `pure`, `elemental`, or `recursive` to define certain characteristics or restrictions on the function.
- `function_name`: This is the name of the function, which you can choose according to your program's naming conventions.
- `(arg1, arg2, ... )`: These are the input arguments of the function. You can specify the number, order, and types of the arguments as needed.
- `result(return_value)`: This specifies the data type of the value returned by the function. The `return_value` is the name of the variable that holds the returned value.
- `variable declarations`: This section is optional and used to declare any local variables needed within the function.
- `executable statements`: These are the statements that define the behavior and calculations performed by the function.

To use a function, you typically call it from another part of the program and assign the returned value to a variable or use it directly in an expression. Functions provide a way to encapsulate specific calculations or operations into reusable units, allowing you to modularize your code and improve readability and maintainability.

---
**Define a function that computes the volume of a cylinder given the radius and height, put the function in a module, and write a main program that calls the function.**

Here's an example of defining a function to compute the volume of a cylinder in Fortran and organizing it within a module:

```fortran
module cylinder_mod
    implicit none
    private          ! Make the contents of the module private  
    public :: cylinder_volume
    contains
    
function cylinder_volume(radius, height) result(volume)
    real, intent(in) :: radius, height
    real             :: volume
    real, parameter :: pi = 3.14159
    volume = pi * radius**2 * height
end function cylinder_volume

end module cylinder_mod

program main
    use cylinder_mod
    implicit none
    
    real :: radius, height, volume
    
    ! Read the values of radius and height from user input or assign them directly
    
    radius = 2.0
    height = 5.0
    
    volume = cylinder_volume(radius, height)
    
    print*, "The volume of the cylinder is:", volume
end program main
```

In this example, the module `cylinder_mod` contains the function `cylinder_volume`, which takes the radius and height of the cylinder as input arguments and returns the calculated volume. The module is then used in the main program, which calls the `cylinder_volume` function with specific values for the radius and height. The resulting volume is then printed to the console.

---
**The program compiles and runs without the `private` statement in the module. In general, why should  you include a `private` statement?**

You are correct that including the `private` statement in a module is not strictly required for the program to compile and run. However, using the `private` statement is considered a good practice in Fortran for several reasons:

1. Encapsulation: By making the module contents private, you are encapsulating the internal details of the module and preventing external access. This helps to enforce modularity and protects the module's implementation details from being inadvertently modified by other parts of the program.

2. Name conflicts: The `private` statement helps to avoid potential naming conflicts between the module's entities (such as functions, subroutines, and variables) and entities with the same name in other parts of the program. It ensures that the module's contents are not inadvertently accessed or overridden outside of the module.

3. Readability and maintainability: Making the module contents private communicates the intended usage and interface of the module. It clarifies which entities are meant to be accessed by other parts of the program (**Note:** those entities are declared `public`.) and which are internal implementation details. This improves the readability and maintainability of the codebase, especially in larger projects with multiple modules.

While including the `private` statement is not strictly required, it is generally recommended to promote code organization, modularity, and prevent potential issues related to naming conflicts.
