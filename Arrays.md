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
