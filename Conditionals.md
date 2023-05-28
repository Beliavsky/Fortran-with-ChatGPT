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
**Explain how the one-line-if statement works and give an example that prints "i is positive" when `i` > 0.**

The general syntax for a one-line conditional statement using the `if` statement in Fortran is:

```fortran
if (condition) action
```

A line that prints "i is positive" when `i` is greater than 0 is

```fortran
if (i > 0) print*, "i is positive"
```

In this example, the `if` statement checks if `i` is greater than 0. If the condition is true, it executes the `print` statement and prints "i is positive". Since the `if` statement is used as a single line, the action to be taken is specified right after the `if` statement.

This approach provides a concise way to conditionally execute a single statement in Fortran when the condition is met.

---
**Explain how the `SELECT CASE` construct works and show a `SELECT CASE` construct that sets the `grade` to "A" when `score` >= 90, "B" when 80 <= `score` < 90, "C" when 70 <= `score` < 80, and "F" otherwise.**

The `SELECT CASE` construct in Fortran provides a way to perform multiple conditional checks on a single expression. It allows you to specify different actions to be taken based on the value of the expression. The general syntax of the `SELECT CASE` construct is as follows:

```fortran
SELECT CASE (expression)
    CASE (value1)
        ! Code block executed when expression matches value1
    CASE (value2)
        ! Code block executed when expression matches value2
    ...
    CASE DEFAULT
        ! Code block executed when no other cases match
END SELECT
```

The `CASE DEFAULT` is optional and serves as a fallback when none of the specified cases match the value of the expression. It ensures that there is a code block to execute even if no other cases match.

The `SELECT CASE` construct provides a structured and readable way to handle multiple conditional checks in Fortran, particularly when dealing with a large number of cases or ranges of values.

Here's an example that uses the `SELECT CASE` construct to set the `grade` based on the given score:

```fortran
program GradeSelector
    implicit none
    integer :: score
    character(len=1) :: grade

    do score = 65, 95, 10
       SELECT CASE (score)
          CASE (90:)
             grade = "A"
          CASE (80:89)
             grade = "B"
          CASE (70:79)
             grade = "C"
          CASE DEFAULT
             grade = "F"
       END SELECT
       print*, "score, grade = ", score, grade
    end do
end program GradeSelector
```

In this example, the `SELECT CASE` construct is used to determine the `grade` based on the value of the `score`. The different cases cover the given score ranges:

- If `score` is 90 or greater, the `grade` is set to "A".
- If `score` is between 80 and 89 (inclusive), the `grade` is set to "B".
- If `score` is between 70 and 79 (inclusive), the `grade` is set to "C".
- If none of the above cases match (i.e., the `score` is below 70 or greater than 90), the `grade` is set to "F" using the `CASE DEFAULT`.

After the `SELECT CASE` construct, the program prints the `score` and the corresponding `grade` to verify the result.

---
**Explain the how the `MERGE` function works and use it to set `result` to "pass" if `grade >= 70` and "fail" otherwise. Use the fact that MERGE is elemental to compute the results for grades = [65, 70, 75].**

The `MERGE` function in Fortran provides a way to selectively combine or merge two values based on a logical condition. It takes three arguments: two values and a logical mask. If the logical mask is `.TRUE.`, the first value is selected; otherwise, the second value is selected.

The general syntax of the `MERGE` function is as follows:

```fortran
MERGE(value1, value2, mask)
```

Here's an example that demonstrates the usage of the `MERGE` function to set `grade` to "pass" if `grade >= 70` and "fail" otherwise:

Certainly! Using the `MERGE` function, we can compute the results for a vector of grades. Here's an example that demonstrates how to compute the results for grades `[65, 70, 75]` using the `MERGE` function in an elemental fashion:

```fortran
program MergeElementalDemo
    implicit none
    integer, dimension(3) :: grades
    character(len=4), dimension(3) :: results
    integer :: i
    
    grades = [65, 70, 75]
    results = MERGE("pass", "fail", grades >= 70)

    do i = 1, size(grades)
        print*, "Grade:", grades(i)
        print*, "Result:", results(i)
    end do

end program MergeElementalDemo
```

In this example, the `grades` array contains the grades `[65, 70, 75]`. By applying the `MERGE` function element-wise on the `grades >= 70` condition, we merge the values "fail" and "pass" based on each grade's eligibility.

The resulting values are stored in the `results` array, where "fail" is selected for grades below 70, and "pass" is selected for grades 70 or higher.

The program then uses a loop to print each grade and its corresponding result.

By leveraging the elemental nature of the `MERGE` function, we can efficiently compute the results for multiple grades without needing explicit loop constructs.

---
