## Conditionals

**How does the `if` statement work?**

The `if` statement in Fortran is a conditional statement used for making decisions based on the truth value of a logical expression. It allows the execution of different code blocks depending on whether the specified condition is true or false.

The basic syntax of the `if` statement in Fortran is as follows:

```fortran
if (condition) then
    ! Code block executed when condition is true
else
    ! Code block executed when condition is false
end if
```

Here's a breakdown of how the `if` statement works:

1. The `condition` is a logical expression that evaluates to either `.true.` or `.false.`. It can involve comparisons (`==`, `/=`, `<`, `>`, `<=`, `>=`), logical operators (`.and.`, `.or.`, `.not.`), or other logical expressions.

2. If the `condition` is true, the code block immediately following the `then` keyword is executed. This code block can contain one or more statements.

3. If the `condition` is false, the code block immediately following the `else` keyword is executed. This code block is optional, and you can omit it if you don't need to handle the false condition separately.

4. The `end if` statement marks the end of the `if` block.

It's important to note that the code blocks within the `if` statement can contain any valid Fortran statements, including assignments, function calls, loops, and subroutine calls.

Additionally, Fortran also supports the `elseif` keyword, which allows you to specify additional conditions to be evaluated if the initial condition is false. This is useful for handling multiple conditions in a structured manner.

Here's an example to demonstrate the usage of the `if` statement:

```fortran
program IfStatementDemo
    implicit none
    integer :: i

    do i = -1, 1
        if (i > 0) then
            print*, "i is positive"
        else if (i < 0) then
            print*, "i is negative"
        else
            print*, "i is zero"
        end if
    end do

end program IfStatementDemo
```

In this code, the variable `i` is looped from -1 through 1 using a `do` loop. Inside the loop, the `if` statement checks the value of `i` and prints the appropriate message based on whether `i` is positive, negative, or zero.

When you run this program, it will print the corresponding messages for each value of `i`, covering all three cases.

---
