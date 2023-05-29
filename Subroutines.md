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

---
**Make the calculate_circle subroutine elemental and pass it radii of 10.0 and 100.0**

To make the `calculate_circle` subroutine elemental, we can modify the code as follows:

```fortran
module CircleModule
    implicit none

    contains

    elemental subroutine calculate_circle(radius, circumference, area)
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

    real :: radii(2), circumference(2), area(2)

    ! Set the radii
    radii = [10.0, 100.0]

    ! Call the elemental subroutine to calculate the circle properties
    call calculate_circle(radii, circumference, area)

    ! Print the results
    print*, "Radii:", radii
    print*, "Circumference:", circumference
    print*, "Area:", area

end program main
```

In this updated code, the `calculate_circle` subroutine has been declared as elemental. It can now accept an array of radii as input and return the corresponding circumferences and areas as arrays. The `radii`, `circumference`, and `area` variables in the main program are now declared as arrays to accommodate the multiple values. The `calculate_circle` subroutine is then called with the `radii` array, and the resulting `circumference` and `area` arrays are printed.

---
**Change the subroutine so that it does not pass circumference and area back as arguments but prints their values, and call it from the main program.**

To modify the `calculate_circle` subroutine to print the circumference and area values instead of passing them back as arguments, we can update the code as follows:

```fortran
module CircleModule
    implicit none

    contains
! ChatGPT-4 initially fails to include the "impure" attribute
    impure elemental subroutine calculate_circle(radius)
        real, intent(in) :: radius
        real, parameter :: pi = 3.14159
        real :: circumference, area

        ! Calculate circumference
        circumference = 2.0 * pi * radius

        ! Calculate area
        area = pi * radius**2

        ! Print the circumference and area
        print*, "Circumference for radius", radius, ":", circumference
        print*, "Area for radius", radius, ":", area
    end subroutine calculate_circle

end module CircleModule

program main
    use CircleModule
    implicit none

    real :: radii(2)

    ! Set the radii
    radii = [10.0, 100.0]

    ! Call the elemental subroutine to calculate and print the circle properties
    call calculate_circle(radii)

end program main
```

In this updated code, the `calculate_circle` subroutine now directly prints the circumference and area values instead of passing them back as arguments. The subroutine receives the radius as an input and performs the calculations accordingly. The `calculate_circle` subroutine is called from the main program with the `radii` array, and it prints the circumference and area for each radius value.

---
**What is an `impure elemental` procedure?**

In Fortran, an `impure elemental` procedure is an elemental procedure that can have side effects. Elemental procedures are those that operate element-wise on arrays or scalar arguments. By default, elemental procedures are pure, meaning they do not have side effects and their output only depends on their input arguments.

However, there are cases where an elemental procedure needs to have side effects, such as printing output or modifying global variables. In such cases, the `impure` attribute can be added to the elemental procedure declaration to indicate that it is impure and can have side effects.

An `impure elemental` procedure allows for element-wise operations while allowing side effects within the procedure body. This can be useful in certain situations where the elemental nature of the procedure is desired, but side effects are necessary.
