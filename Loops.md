## Loops

**How do loops work?**

Loops in Fortran are constructs that allow for a sequence of instructions to be executed repeatedly. There are several types of loops in Fortran, but the most commonly used is the `do` loop, which is similar to `for` loops in other languages.

Here's the basic syntax of a `do` loop:

```Fortran
do i = start, end, step
    ! Instructions to be repeated
end do
```

- `i` is the loop control variable. It takes on each integer value from `start` to `end`, in increments of `step`. If `step` is omitted, it defaults to 1.
- `start`, `end`, and `step` are integer expressions.
- The instructions inside the loop (between `do` and `end do`) are executed once for each value of `i`.

Here's an example:

```Fortran
program LoopDemo
    implicit none
    integer :: i

    do i = 1, 5
        print*, 'Iteration number: ', i
    end do

end program LoopDemo
```

In this program, the `do` loop iterates over the values 1 to 5. Each time through the loop, it prints the current iteration number.

In addition to the `do` loop, Fortran also supports the `do while` loop, which repeats a block of code while a certain condition is true. Here's the basic syntax:

```Fortran
do while (condition)
    ! Instructions to be repeated
end do
```

- `condition` is a logical expression.
- The instructions inside the loop are executed repeatedly as long as `condition` is true.

Here's an example:

```Fortran
program LoopDemo
    implicit none
    integer :: i

    i = 1
    do while (i <= 5)
        print*, 'Iteration number: ', i
        i = i + 1
    end do

end program LoopDemo
```

In this program, the `do while` loop repeats as long as `i` is less than or equal to 5. Each time through the loop, it prints the current iteration number and then increments `i` by 1.

---
**Can the test to exit the loop not be at the beginning?**

Yes, Fortran has the `exit` and `cycle` statements that can be used to control the flow of a loop from within the body, not just at the beginning.

The `exit` statement is used to exit a loop prematurely. It can be used in any type of loop (`do`, `do while`, or even named loops). When the `exit` statement is encountered, the program immediately exits the loop, and execution continues with the statement following the `end do`.

Here's an example:

```Fortran
program LoopDemo
    implicit none
    integer :: i

    do i = 1, 10
        if (i > 5) then
            exit
        end if
        print*, 'Iteration number: ', i
    end do

end program LoopDemo
```

In this program, the `do` loop starts to iterate over the values 1 to 10. But if `i` is greater than 5, the `exit` statement is executed, and the loop is exited prematurely. So, this program only prints the iteration number for `i` from 1 to 5.

The `cycle` statement is used to skip the remainder of the current iteration and move on to the next iteration of the loop. When the `cycle` statement is encountered, the program immediately jumps to the next iteration of the loop, skipping any statements that follow `cycle` in the loop body.

Here's an example:

```Fortran
program LoopDemo
    implicit none
    integer :: i

    do i = 1, 5
        if (i == 3) then
            cycle
        end if
        print*, 'Iteration number: ', i
    end do

end program LoopDemo
```

In this program, the `do` loop iterates over the values 1 to 5. But if `i` is equal to 3, the `cycle` statement is executed, and the loop moves on to the next iteration, skipping the `print` statement. So, this program prints the iteration number for `i` equal to 1, 2, 4, and 5, but not 3.

---
**How do loops in Fortran differ from those in C and C++?**

Fortran's loops are conceptually similar to those in C and C++, but there are some differences in the syntax and behavior due to the differences in the language designs.

Here are some key differences:

1. **Syntax:** In C and C++, the `for` loop syntax is `for(initialization; condition; increment)`. In Fortran, the `do` loop syntax is `do variable = start, end, increment`. The increment in Fortran loop is optional and defaults to 1, while in C/C++, if not specified, there's no implicit increment.

2. **Loop variable mutation:** In Fortran, changing the loop variable inside the loop is considered bad practice (**Note:** it violates the Fortran standard) and does not affect the number of iterations, while in C/C++, it's possible to change the loop variable within the loop which will affect the iteration.

3. **Zero iterations:** In Fortran, if the end value is less than the start value in a `do` loop, the loop body will not execute at all, i.e., it results in zero iterations. In C/C++, a `for` loop will always execute at least once unless the condition is false at the start.

4. **Exit and Cycle:** Fortran has `exit` and `cycle` statements for breaking out of the loop and skipping to the next iteration respectively. C and C++ have similar keywords (`break` and `continue`).

5. **Named loops:** Fortran allows you to name your loops, which is useful for nested loops where you might want to break out of or cycle not just the innermost loop, but an outer loop. C and C++ do not have an equivalent feature.

Despite these differences, loops in both languages serve the same purpose: to repeatedly execute a block of code. The differences are largely due to the differing design philosophies and the different problem domains the languages are designed to address.
