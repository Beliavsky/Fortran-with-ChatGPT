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
**Explain how the `WHERE` construct works and use it to set `grades` based on `scores` using the same rule as in the previous GradeSelector program, for `grades` = [65, 75, 85, 95].**

The `WHERE` construct in Fortran provides a way to selectively assign values to an array based on a logical condition. It allows you to perform an element-wise assignment to an array using a mask that specifies which elements of the array should be updated.

The general syntax of the `WHERE` construct is as follows:

```fortran
WHERE (mask)
    array = expression
[ELSEWHERE (mask)]
    array = expression
END WHERE
```

Here's an example that demonstrates the usage of the `WHERE` construct to set `grades` based on `scores` using the same rule as in the previous `GradeSelector` program, with `grades = [65, 75, 85, 95]`:

```fortran
program WhereDemo
    implicit none
    integer, dimension(4) :: scores
    character(len=1), dimension(4) :: grades
    integer :: i

    scores = [65, 75, 85, 95]

    WHERE (scores >= 90)
        grades = "A"
    ELSEWHERE (scores >= 80)
        grades = "B"
    ELSEWHERE (scores >= 70)
        grades = "C"
    ELSEWHERE
        grades = "F"
    END WHERE

    do i = 1, size(scores)
        print*, "Score:", scores(i)
        print*, "Grade:", grades(i)
    end do

end program WhereDemo
```

In this example, the `scores` array contains the scores `[65, 75, 85, 95]`. The `WHERE` construct is used to conditionally assign values to the `grades` array based on the scores.

If a score is greater than or equal to 90, the corresponding grade is set to 95. If it's between 80 and 89, the grade is set to 85. If it's between 70 and 79, the grade is set to 75. And for any score below 70, the grade is set to 65.

The program then uses a loop to print each score and its corresponding grade.

The `WHERE` construct provides a concise and efficient way to assign values to an array based on logical conditions, making it particularly useful when dealing with element-wise operations.

---
**Does Fortran short circuit when evaluating logical expressions? For example, for array `x` with lower bound of 1, is it safe to write**
```
if (i > 0 .and. x(i) > 0) print*,"for i =", i, " x(i) is positive"
```

<details>
  <summary>After giving a wrong answer and being corrected</summary>
    
In Fortran, logical expressions are evaluated using short-circuit evaluation. Short-circuit evaluation means that the logical operators `AND` and `OR` do not evaluate the second operand if the result can be determined solely based on the value of the first operand.

In your example code:

```fortran
if (i > 0 .and. x(i) > 0) print*,"for i =", i, " x(i) is positive"
```

The `AND` operator will short-circuit if `i > 0` is `FALSE` because the entire expression will be `FALSE` regardless of the value of `x(i)`. This means that if `i` is not greater than 0, the evaluation will stop at that point, and the condition `x(i) > 0` will not be evaluated.

Therefore, it is safe to write the code as shown. If `i > 0` is `FALSE`, the condition `x(i) > 0` will not be evaluated, preventing any potential issues with accessing `x(i)` when `i` is out of bounds or undefined.

Short-circuit evaluation helps improve efficiency and avoid potential errors in cases where the evaluation of the second operand is unnecessary based on the result of the first operand.
    
**This is wrong. You cannot count on short-circuiting.**
</details>

**ChatGPT-4 says**

Apologies for the incorrect information provided earlier. You are correct. In Fortran, the standard does not guarantee short-circuit evaluation for logical expressions. Therefore, it is safer to explicitly separate the conditions and use separate `IF` statements for each condition to ensure the desired behavior. Here is the corrected code:

```fortran
if (i > 0) then
    if (x(i) > 0) then
        print*,"for i =", i, " x(i) is positive"
    end if
end if
```

By separating the conditions into individual `IF` statements, you can ensure that the second condition is only evaluated when the first condition is satisfied.

    
    

