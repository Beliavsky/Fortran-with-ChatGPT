## Subroutines

**How do subroutines work? When should they be used instead of functions?**

Subroutines in Fortran are procedures that perform a specific task or a series of actions. They allow you to group a sequence of statements together and execute them as a unit. Unlike functions, subroutines do not return a value, but they can modify the values of variables passed to them as arguments.

Here's how subroutines work in Fortran:

1. Procedure definition: You define a subroutine by declaring its name, specifying the input and output arguments (if any), and providing the sequence of statements to be executed. The subroutine definition typically starts with the `subroutine` keyword, followed by the subroutine name and the list of arguments.

2. Argument passing: Subroutines can receive input arguments, output arguments, or both. Input arguments are passed to the subroutine to provide data for computation, while output arguments are used to return modified values back to the caller.

3. Procedure call: To execute a subroutine, you call it by its name and provide the necessary arguments. The values of the arguments are passed to the subroutine, where they can be used and modified as needed. After the subroutine completes its execution, control returns to the caller.

4. Modifying variables: Unlike functions, subroutines do not have a specific return value. Instead, they can modify variables passed to them by reference. Any changes made to the variables within the subroutine will be reflected in the caller's scope.

Subroutines should be used when you need to perform a series of actions or modify multiple variables without the need to return a specific value. Here are some scenarios where subroutines are commonly used:

1. Performing calculations or operations that do not require returning a result.
2. Modifying the state of variables or data structures.
3. Executing a series of actions or statements.
4. Encapsulating complex or repetitive code segments for reusability.

In contrast, functions should be used when you need to compute and return a specific result. Functions are suitable when you require a value based on the given input arguments without any side effects or modifications to other variables. Functions are typically used for calculations, data transformations, or evaluations.

It's worth noting that subroutines and functions can work together, where a function can be called within a subroutine to compute a value and then modify variables based on the result. This allows for a modular and organized programming approach, separating the responsibilities of computation and variable modification.

To summarize, subroutines are used when you need to perform a series of actions or modify variables without returning a specific value. They are suitable for operations that require side effects or state modifications. Functions, on the other hand, are used when you need to compute and return a specific result based on the input arguments.

---
**Write a `pure` subroutine that calculates the circumference and area of a circle with a given radius. Put in a module and call it from a main program.**

ChatGPT-4 initially errs by saying that subroutines cannot be `pure`. When corrected, it produces this code:

```fortran
module CircleModule
    implicit none

    contains

    pure subroutine calculate_circle(radius, circumference, area)
        real, intent(in) :: radius
        real, intent(out) :: circumference, area
        real, parameter :: pi = 3.14159

        ! Calculate circumference
        circumference = 2.0 * pi * radius

        ! Calculate area
        area = pi * radius**2
    end subroutine calculate_circle

end module CircleModule

program main
    use CircleModule
    implicit none

    real :: radius, circumference, area

    ! Set the radius
    radius = 5.0

    ! Call the pure subroutine to calculate the circle properties
    call calculate_circle(radius, circumference, area)

    ! Print the results
    print*, "Radius:", radius
    print*, "Circumference:", circumference
    print*, "Area:", area

end program main
```
