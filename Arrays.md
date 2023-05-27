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
**How do I refer to the elements of a 1-D array x in reverse order?**

To refer to the elements of a 1-D array `x` in reverse order, you can use array sections with a negative stride. Here's an example:

```fortran
x(size(x):1:-1)
```

In this example, `x(size(x):1:-1)` creates an array section that starts from the last element of `x` and goes to the first element in reverse order. The resulting array section will contain the elements of `x` in reverse order.

You can use this array section in assignments, computations, or any other operations involving the reversed elements of `x`. **Note:** if `x` has a lower bound other than 1, use `x(ubound(x):lbound(x):-1)`

---
**How do I refer to an arbitrary collection of indices of an array, for example elements 2, 3, and 5 of 1-D array x?**

In Fortran, you can use an array section to refer to an arbitrary collection of indices of an array. To refer to elements 2, 3, and 5 of a 1-D array `x`, you can use the following syntax:

```fortran
x([2, 3, 5])
```

This creates an array section that consists of the specified indices. The resulting array section will have the values of elements 2, 3, and 5 of `x`. You can use this array section in assignments, computations, or any other operations involving the selected elements.

---
**Generalizing this, if x is a 2-D array, how do I refer to a subset of x determined by specified row and column indices?**

To refer to a subset of a 2-D array `x` determined by specified row and column indices, you can use array sections along both dimensions. Here's an example:

```fortran
x([2, 3], [1, 3, 4])
```

In this example, the array section `x([2, 3], [1, 3, 4])` selects rows 2 and 3 and columns 1, 3, and 4 of `x`. The resulting array section will have the values of the selected elements from `x`. 

You can use this array section in assignments, computations, or any other operations involving the selected subset of `x`.

---
**How do I get the elements of array x satisfying a condition, for example being positive?**

ChatGPT gives a wrong answer. The right answer is to use `pack` intrinsic function, as in the expression
```
pack(x, mask = x > 0)
```

---
**How would I count the number of elements of array x that satisfy a condition, for example being positive?**
To count the number of elements in an array `x` that satisfy a specific condition, such as being positive, you can use the `COUNT` intrinsic function, which returns the number of elements in an array that meet a specified condition.

Here's an example of how you can count the number of positive elements in an array `x`:

```fortran
program count_positive_elements
    implicit none
    integer, parameter :: n = 10
    real :: x(n)
    
    ! Initialize array x with some values
    x = [1.0, -2.0, 3.0, -4.0, 5.0, -6.0, 7.0, -8.0, 9.0, -10.0]
    
    ! Print the number of positive elements in x
    print *, "Number of positive elements:", count(x > 0.0) ! 5
end program count_positive_elements
```

In this example, the `x > 0.0` expression creates a logical mask indicating which elements of `x` are positive. The `count` function is then used to count the number of `True` values in the mask, which corresponds to the number of positive elements in `x`.

---
**Given two 1-D arrays x and y of the same type, how do I concatenate them, creating a 1-D array containing the elements of x followed by those of y?**

ChatGPT-4 gives a wrong answer. Concatenate `x` and `y` by putting them in an array constructor, as with

```Fortran
combined = [x, y] ! size(combined) = size(x) + size(y)
```

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

---
**How would I print the sum of the squares of the elements of x in the code above?**

To print the sum of the squares of the elements of array `x`, you can use the `sum` function in combination with the exponentiation operator (`**`):

```fortran
write(*, *) "Sum of squares:", sum(x**2)
```

This line calculates the squares of each element of `x` using the exponentiation operator `**`, and then uses the `sum` function to compute the sum of the squared values. The result is printed using the `write` statement.

---
**How do I declare an array with more than one dimension?**

Declaring an array with more than one dimension in Fortran is straightforward. The syntax is similar to declaring a one-dimensional array, but you provide multiple dimension specifications, separated by commas. 

Here's an example of a two-dimensional array:

```Fortran
integer, dimension(3, 4) :: myArray
```

In this declaration, `myArray` is a two-dimensional array with 3 rows and 4 columns.

Here's an example of a three-dimensional array:

```Fortran
real, dimension(4, 5, 6) :: myArray
```

In this declaration, `myArray` is a three-dimensional array with dimensions 4, 5, and 6.

You can also specify the lower and upper bounds of each dimension. For example:

```Fortran
integer, dimension(-1:2, 0:3) :: myArray
```

In this declaration, `myArray` is a two-dimensional array. The first dimension goes from -1 to 2 (so it has 4 elements), and the second dimension goes from 0 to 3 (so it also has 4 elements).

You can initialize multi-dimensional arrays at the time of declaration, using nested array constructors. Here's an example:

```Fortran
integer, dimension(2, 2) :: myArray = reshape([1, 2, 3, 4], [2, 2])
```

In this declaration, `myArray` is a 2x2 array that is initialized with the values 1, 2, 3, and 4. The `reshape` function is used to shape a one-dimensional array into the desired multi-dimensional array shape.

**Note:** there is alternative declaration syntax that does not use `dimension`, for example
```Fortran
integer :: myArray(3, 4)
```

---
**How do I refer to a single element of a multidimensional array?**

To refer to a single element of a multidimensional array in Fortran, you can use the array indices separated by commas. The general syntax is `array(index1, index2, ..., indexN)`, where `array` is the name of the array and `index1, index2, ..., indexN` are the indices corresponding to each dimension of the array.

Here's an example:

```fortran
integer, dimension(3, 4) :: matrix
matrix(2, 3) = 42  ! Assign a value to the element at row 2, column 3
```

In this example, `matrix` is a 2D array with dimensions 3 and 4. The statement `matrix(2, 3) = 42` assigns the value 42 to the element located at the second row and third column of the array.

You can use the same indexing syntax to access or modify elements of multidimensional arrays in Fortran.

---
**For a 2-D array, in other words a matrix, how would I refer to a single row or column?**

In Fortran, you can refer to a single row or column of a two-dimensional array (a matrix) using the colon `:` operator.

Here's an example for a single row:

```Fortran
integer, dimension(3,4) :: myArray
integer, dimension(4) :: myRow

myRow = myArray(2, :)
```

In this example, `myArray(2, :)` refers to the second row of `myArray`. The `:` operator is used to select all elements along the second (column) dimension, so `myArray(2, :)` includes all columns of the second row.

For a single column, you would do this:

```Fortran
integer, dimension(3,4) :: myArray
integer, dimension(3) :: myColumn

myColumn = myArray(:, 3)
```

In this example, `myArray(:, 3)` refers to the third column of `myArray`. The `:` operator is used to select all elements along the first (row) dimension, so `myArray(:, 3)` includes all rows of the third column.

Remember that Fortran is a column-major language, which means that the first index is the row index, and the second index is the column index. This is the opposite of row-major languages like C and Python.

---
**How do I compute the sum of each column of an array, or the sum of each row?**

To compute the sum of each column or each row of an array in Fortran, you can use the intrinsic function `SUM` with appropriate dimensions specified.

To compute the sum of each column, you can use the `SUM` function along with the `DIM` argument set to 1. Here's an example:

```fortran
integer, dimension(3, 4) :: matrix
integer, dimension(4) :: column_sum

! ... Initialize matrix with values ...

! Compute the sum of each column
column_sum = SUM(matrix, dim=1)
```

In this example, `matrix` is a 2D array with dimensions 3 and 4. The `SUM` function is used with `dim=1` to calculate the sum along the first dimension (columns), resulting in a 1D array `column_sum` of size 4. Each element of `column_sum` will contain the sum of the corresponding column of `matrix`.

Similarly, to compute the sum of each row, you can use the `SUM` function with `dim=2`. Here's an example:

```fortran
integer, dimension(3, 4) :: matrix
integer, dimension(3) :: row_sum

! ... Initialize matrix with values ...

! Compute the sum of each row
row_sum = SUM(matrix, dim=2)
```

In this case, `SUM` is used with `dim=2` to calculate the sum along the second dimension (rows), resulting in a 1D array `row_sum` of size 3. Each element of `row_sum` will contain the sum of the corresponding row of `matrix`.

---
**What are some other intrinsic array functions with an optional DIM argument?**

In addition to the `SUM` function, there are several other intrinsic array functions in Fortran that have an optional `DIM` argument. Some of the commonly used ones include:

- `PRODUCT`: Calculates the product of array elements along a specified dimension.
- `MAXVAL`: Finds the maximum value among array elements along a specified dimension.
- `MINVAL`: Finds the minimum value among array elements along a specified dimension.
- `COUNT`: Counts the number of elements that satisfy a specified condition along a specified dimension.
- `ALL`: Checks if all elements satisfy a specified condition along a specified dimension.
- `ANY`: Checks if any element satisfies a specified condition along a specified dimension.

These functions provide flexibility in performing various calculations on arrays along specific dimensions, allowing you to obtain results such as sums, products, maximum/minimum values, counts, and more.

For detailed information about these functions and their usage, you can refer to the Fortran language documentation or a Fortran programming guide.

---
**Given a possibly multidimensional array x, how do you get the size along each axis and the total size?**

To get the size along each dimension and the total size of a multidimensional array `x` in Fortran, you can use the `SIZE` intrinsic function. Here's an example:

```fortran
program array_size
    implicit none
    
    real, dimension(3, 4, 2) :: x
    
    integer :: size_dim1, size_dim2, size_dim3, total_size
    
    size_dim1 = size(x, dim=1)
    size_dim2 = size(x, dim=2)
    size_dim3 = size(x, dim=3)
    total_size = size(x)
    
    print *, "Size along dimension 1:", size_dim1
    print *, "Size along dimension 2:", size_dim2
    print *, "Size along dimension 3:", size_dim3
    print *, "Total size:", total_size
    print *, "Shape:", shape(x) ! line added by me, returns [3, 4, 2]
end program array_size
```

In this example, the `SIZE` function is used to obtain the sizes of `x` along each dimension (`dim=1`, `dim=2`, `dim=3`) and the total size (`size(x)`). The results are then printed to the console. **Note:** the `SHAPE` function returns an array of the sizes along each dimension.

---
**How do I get the lower and upper bounds of array x along each dimension?**

To get the lower and upper bounds of an array `x` along each dimension, you can use the `LBOUND` and `UBOUND` intrinsic functions. Here's an example of how you can obtain the lower and upper bounds along each dimension:

```fortran
program array_bounds
    implicit none
    
    real, dimension(-2:3, 1:4, 5:8) :: x
    
    integer :: lb_dim1, ub_dim1
    integer :: lb_dim2, ub_dim2
    integer :: lb_dim3, ub_dim3
    
    lb_dim1 = lbound(x, dim=1)
    ub_dim1 = ubound(x, dim=1)
    
    lb_dim2 = lbound(x, dim=2)
    ub_dim2 = ubound(x, dim=2)
    
    lb_dim3 = lbound(x, dim=3)
    ub_dim3 = ubound(x, dim=3)
    
    print *, "Lower bound of dimension 1:", lb_dim1 ! -2
    print *, "Upper bound of dimension 1:", ub_dim1 !  3
    
    print *, "Lower bound of dimension 2:", lb_dim2 !  1
    print *, "Upper bound of dimension 2:", ub_dim2 !  4
    
    print *, "Lower bound of dimension 3:", lb_dim3 !  5
    print *, "Upper bound of dimension 3:", ub_dim3 !  8
    ! 2 lines below added by me
    print *, "Lower bounds:", lbound(x) ! -2  1  5
    print *, "Upper bounds:", ubound(x) !  3  4  8
end program array_bounds
```

In this example, the `LBOUND` function is used to obtain the lower bounds of `x` along each dimension (`dim=1`, `dim=2`, `dim=3`), and the `UBOUND` function is used to obtain the upper bounds. **Note:** `LBOUND` and `UBOUND` without a `dim` argument return arrays containing the lower and upper bounds along the dimensions.

---
**What is the most concise way to print all the elements of an array in a single statement? In what order will the elements be printed?**

Here's an example of how you can achieve this concisely:

```fortran
program print_array
    implicit none
    integer :: i, j
    integer, parameter :: n = 3, m = 4
    integer :: array(n, m)    

    ! Assign values to the array
    array = reshape([((i+j, i=1,n), j=1,m)], shape(array))
  
    ! Print the elements of the array in a single statement
    print *, array
    
end program print_array
```

In this example, `print *, array` will print all the elements of the array in a single statement. The elements will be printed column-wise from top to bottom, following the column-major storage order.

---
**Explain what the following line of code does:**
```
array = reshape([((i+j, i=1,n), j=1,m)], shape(array))
```

The line of code `array = reshape([((i+j, i=1,n), j=1,m)], shape(array))` reshapes a one-dimensional array created using an array constructor into a two-dimensional array `array` with dimensions `n` rows and `m` columns.

Let's break down the line of code:

1. `((i+j, i=1,n), j=1,m)` creates a one-dimensional array using nested loops. It generates values `i+j` for each combination of `i` and `j` ranging from `1` to `n` and `1` to `m`, respectively. The result is a one-dimensional array of length `n*m` with values `[2, 3, 4, ..., n+m-1]`.

2. `[((i+j, i=1,n), j=1,m)]` creates an array constructor with a single expression, which is the one-dimensional array generated in step 1. The outer square brackets `[]` denote an array constructor.

3. `reshape([...], shape(array))` reshapes the one-dimensional array inside the array constructor into the shape specified by `shape(array)`. The `shape` function retrieves the shape (dimensions) of the target array `array`. The reshaping operation converts the one-dimensional array into a two-dimensional array with dimensions `n` rows and `m` columns.

4. Finally, `array = reshape([...], shape(array))` assigns the reshaped array to the variable `array`, effectively populating it with the values generated in step 1.

In summary, the line of code creates a two-dimensional array `array` with dimensions `n` rows and `m` columns, and populates it with values computed based on the row and column indices.

---
**What are the intrinsic functions for linear algebra?**

Some commonly used intrinsic functions for linear algebra functions are

   - `MATMUL(a, b)`: Computes the matrix-matrix or matrix-vector product of `a` and `b`.
   - `DOT_PRODUCT(a, b)`: Computes the dot product of two vectors `a` and `b`.
   - `TRANSPOSE(matrix)`: Computes the transpose of a matrix.

