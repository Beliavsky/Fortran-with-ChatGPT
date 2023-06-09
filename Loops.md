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
**For a loop**
```
do i=1,n
   ...
end do
print*,i
```
**what value will be printed for i if the loop is not exited early?**

If the loop is not exited early and completes all iterations, the value of `i` printed after the loop will be the value of `n + 1`. 

In a Fortran `do` loop, the loop variable (`i` in this case) is incremented after each iteration until it reaches the value specified in the `do` statement. When the loop condition evaluates to false, the loop is terminated, and the loop variable takes on the next value after the loop condition becomes false. In this case, the loop variable `i` will be incremented to `n + 1` before the loop terminates, and that will be the value printed after the loop.

Here's an example to illustrate this behavior:

```fortran
program main
  implicit none
  integer :: i, n

  n = 5

  do i = 1, n
    ! Loop body
  end do

  print*, i  ! Prints n + 1

end program main
```

If `n` is 5, the loop will execute 5 times, and the value of `i` printed after the loop will be 6.

---
**How do nested loops work? If you use an exit statement in a nested loop, how do you control which loop you exit?**

Nested loops in Fortran work similarly to nested loops in most other programming languages. In a nested loop, one loop (the inner loop) is contained within another loop (the outer loop). Each time through the outer loop, the inner loop goes through all its iterations.

Here's a simple example:

```Fortran
program NestedLoopDemo
    implicit none
    integer :: i, j

    do i = 1, 3
        do j = 1, 3
            print*, 'i = ', i, ', j = ', j
        end do
    end do

end program NestedLoopDemo
```

In this program, there are two loops. The outer loop (controlled by `i`) goes from 1 to 3. Each time through the outer loop, the inner loop (controlled by `j`) also goes from 1 to 3. So, the `print` statement is executed 9 times in total, with each combination of `i` and `j`.

To control which loop is exited when an `exit` statement is encountered, you can use named loops. A named loop is a loop that has a name assigned to it. You can exit a named loop from within a nested loop by using the `exit` statement followed by the name of the loop.

Here's an example:

```Fortran
program NamedLoopDemo
    implicit none
    integer :: i, j

    outerLoop: do i = 1, 3
        innerLoop: do j = 1, 3
            if (j == 2) then
                exit outerLoop
            end if
            print*, 'i = ', i, ', j = ', j
        end do innerLoop
    end do outerLoop

end program NamedLoopDemo
```

In this program, the loops are named `outerLoop` and `innerLoop`. When `j` equals 2, the `exit outerLoop` statement is executed, which exits the outer loop prematurely. So, the `print` statement is only executed for `i` equals 1, and `j` equals 1.

Without a loop name after the `exit` statement, the program would only exit the inner loop, not the outer loop. This is the value of named loops when dealing with nested loops and complex loop control.

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

---
**In Python with NumPy, R, and Matlab, you are advised to favor array operations over loops for speed. What about in Fortran? Do you have advice on using loops efficiently?**

In Fortran, the situation is somewhat different than in interpreted languages like Python and R or environments like MATLAB. These environments often advocate for "vectorized" operations (i.e., operations on entire arrays) because loops in these languages tend to be slow due to their interpreted nature. In Fortran, a compiled language, loops are highly optimized by the compiler and are typically fast. 

However, Fortran also supports array operations (also known as "array programming" or "vectorization"), which allow you to operate on whole arrays at once without writing explicit loops. These can be easier to read and write, and can sometimes be faster due to exploiting low-level optimizations and parallelism. 

In general, efficient usage of loops and arrays in Fortran often comes down to a few principles:

1. **Understand Your Compiler:** Modern Fortran compilers can often optimize loops very effectively, particularly if you enable the appropriate optimization flags. Understanding how your compiler optimizes code can help you write more efficient loops.

2. **Exploit Array Operations Where Possible:** While loops are efficient in Fortran, array operations can be more readable and can sometimes be faster due to low-level optimizations and parallel processing.

3. **Access Patterns:** When dealing with multi-dimensional arrays, try to access data in a manner that's consistent with the array's storage order in memory. Fortran uses column-major ordering, meaning it stores multi-dimensional arrays in a way where the first index changes fastest. 

4. **Parallelism:** Modern Fortran has built-in support for parallelism, both via shared-memory parallelism (OpenMP) and distributed-memory parallelism (MPI). If you have a high-performance computing system available, you can use these features to spread your loop iterations over multiple processors or cores.

Remember, the best approach can depend heavily on the specific problem you're trying to solve, the specific compiler you're using, and the specific system you're running on. When in doubt, profiling your code to see where the performance bottlenecks actually are can be very helpful.
