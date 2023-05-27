## Arrays

---
**What are arrays?**

In Fortran, as in many other programming languages, an array is a collection of elements that are all of the same type (e.g., integer, real, etc.) and that can be accessed via an index. Each element in the array is a variable that can hold a value. 

Arrays are very useful in programming because they allow you to work with many related values at once, using a single name and an index to refer to a specific value. For example, you might use an array to store the grades of all students in a class, or the temperatures measured every day in a month.

In Fortran, arrays can be one-dimensional (like a vector), two-dimensional (like a matrix), or more. The size of the array must be declared when the array is created.

Here is an example of a one-dimensional array in Fortran:

```Fortran
program ArrayDemo
    implicit none
    integer, dimension(5) :: myArray
!   Note: the line below is equivalent
!   integer :: myArray(5) 
    myArray = [1, 2, 3, 4, 5]
    print*, 'The array: ', myArray
end program ArrayDemo
```

In this program, `myArray` is a one-dimensional array that can hold 5 integers. The `dimension(5)` part of the declaration specifies the size of the array. The array is then filled with the values 1 through 5 using an array constructor (`[...]`).

You can access individual elements of the array using their index, like so:

```Fortran
print*, 'The first element: ', myArray(1)
print*, 'The third element: ', myArray(3)
```

Note that Fortran, unlike some other programming languages such as C and Python, uses 1-based indexing (**Note:** this is the default, which can be overridden). That is, the first element of the array is `myArray(1)`, not `myArray(0)`.

---
**How do you set all the values of an array to a single value?**

<details>
  <summary>After giving a wrong answer and being corrected</summary>

To set all the values of an array to a single value in Fortran, you can use the intrinsic function `fill`, which fills an array with a specified value. Here's an example:

```fortran
integer, dimension(5) :: arr
arr = fill(10, size(arr))
```

In this example, the array `arr` is declared as an integer array of size 5. The `fill` function is used to assign the value `10` to all elements of `arr`. The `size` function is used to determine the size of the array, which is then passed as the second argument to `fill`.

After executing this code, all elements of the array `arr` will be set to the value `10`.
    
**No, you would just write "arr = 10" instead of the above. Fortran does not have an intrinsic fill() function.**
</details>

**ChatGPT-4 says**

You can directly assign a single value to all elements of an array using the assignment statement, for example:

```
integer, dimension(5) :: arr
arr = 10
```

In this example, the value `10` is assigned to all elements of the array `arr`.

---
**How do you set N elements of an array to N distinct values, say x(1:3) to 2, 3, and 5?**

To set N elements of an array to N distinct values, you can use array assignment with an array literal. Here's an example of setting `x(1:3)` to the values 2, 3, and 5:

```
integer, dimension(3) :: x
x = [2, 3, 5]
```

In this example, the array literal `[2, 3, 5]` contains the values that will be assigned to the corresponding elements of `x(1:3)`.

You can adjust the size and values in the array literal based on your specific needs. (**Note:** an equivalent syntax, and the only one allowed in Fortran 90, to use `(/ /)` to enclose the array elements, for example `x = (/2, 3, 5/)`.)

---
**What if variable x is declared as**
```
real :: x(5)
```
**and you try to access an element of x with subscript outside the range of 1 through 5?**

If you try to access an element of an array with a subscript (index) that is outside the declared range of the array, your program will likely crash or produce unexpected results. 

In Fortran, array bounds are checked at runtime. If you try to access an array element that is outside the valid range, you'll usually get a runtime error. 

For example, consider this Fortran program:

```Fortran
program ArrayDemo
    implicit none
    real :: x(5)

    x = [1.0, 2.0, 3.0, 4.0, 5.0]
    print*, 'Sixth element of x: ', x(6)
end program ArrayDemo
```

This program will typically crash when it tries to access `x(6)`, because `x` only has 5 elements. The exact error message you'll see depends on your Fortran compiler and runtime environment, but it might look something like this:

```
Fortran runtime error: Index '6' of dimension 1 of array 'x' above upper bound of 5
```

To avoid these kinds of errors, you should always make sure that your code never tries to access an array element outside of its valid range. You can do this by using array bounds in loops and other control structures, and by validating any user input or other data that's used as an array index.

---
**How do you refer to only part of an array?**

In Fortran, you can refer to a portion of an array using array sections. This is a very powerful feature that allows you to operate on subsets of an array without having to write explicit loops.

Array sections are specified by providing a range of indices instead of a single index. The range is written as `start:end`, where `start` is the index of the first element in the section and `end` is the index of the last element. Here's an example:

```Fortran
program ArraySection
    implicit none
    integer, dimension(10) :: myArray
    integer :: i

    ! Initialize the array
    myArray = [(i, i = 1, 10)]

    ! Print the whole array
    print*, 'The whole array: ', myArray

    ! Print a section of the array
    print*, 'Elements 3 to 6: ', myArray(3:6)
end program ArraySection
```

In this program, `myArray(3:6)` refers to a section of `myArray` that includes elements 3, 4, 5, and 6. 

You can also use array sections on the left-hand side of an assignment to modify a portion of an array. For example:

```Fortran
myArray(3:6) = 0
```

This statement sets elements 3, 4, 5, and 6 of `myArray` to zero.

Furthermore, you can use a stride value to refer to every nth element in an array section. The syntax for this is `start:end:stride`. For example:

```Fortran
print*, 'Every second element from 3 to 9: ', myArray(3:9:2)
```

This statement prints elements 3, 5, 7, and 9 of `myArray`.

Array sections are a powerful tool for writing concise and efficient Fortran code, especially when working with large, multidimensional arrays. However, it's important to remember that, like any tool, they should be used judiciously and with an understanding of their potential impact on performance.

---
**If I have an array of data, say x = [20.0, 30.0, 40.0, 10.0], how do I calculate things like the sum, product, minimum, or maximum of the array? How do I find the positions of the smallest and largest elements? Illustrate with one program.**

Here's an example program in Fortran that calculates the sum, product, minimum, maximum, and positions of the smallest and largest elements in an array:

```Fortran
program array_operations
    implicit none
    
    real, dimension(4) :: x = [20.0, 30.0, 40.0, 10.0]
    real :: sum_x, product_x
    real :: min_x, max_x
    integer :: min_index, max_index
    
    ! Calculate the sum of the array
    sum_x = sum(x)
    
    ! Calculate the product of the array
    product_x = product(x)
    
    ! Find the minimum and its position
    min_x = minval(x)
    min_index = minloc(x, dim=1) ! Initially ChatGPT-4 forgot the dim argument and the program did not compile
    
    ! Find the maximum and its position
    max_x = maxval(x)
    max_index = maxloc(x, dim=1)
    
    ! Print the results
    write(*, *) "Array:", x
    write(*, *) "Sum:", sum_x
    write(*, *) "Product:", product_x
    write(*, *) "Minimum:", min_x, "at position", min_index
    write(*, *) "Maximum:", max_x, "at position", max_index
    
end program array_operations
```
