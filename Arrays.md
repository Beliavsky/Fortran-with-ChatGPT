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
