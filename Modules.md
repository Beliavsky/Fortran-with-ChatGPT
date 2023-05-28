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
