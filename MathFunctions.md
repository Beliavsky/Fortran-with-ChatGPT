## Math Functions

**What are the most important built-in math functions?**

Fortran offers a broad range of built-in mathematical functions. Here are some of the most commonly used ones:

1. **Power:** `a**b` computes `a` to the power of `b`.

2. **Square root:** `sqrt(x)` returns the square root of `x`.

3. **Exponential and Logarithm:**
   - `exp(x)` computes the exponential of `x` (i.e., `e**x`).
   - `log(x)` computes the natural logarithm of `x`.
   - `log10(x)` computes the base-10 logarithm of `x`.

4. **Trigonometry:**
   - `sin(x)`, `cos(x)`, `tan(x)` compute the sine, cosine, and tangent of `x`, respectively, where `x` is in radians.
   - `asin(x)`, `acos(x)`, `atan(x)` compute the inverse sine (arcsine), cosine (arccosine), and tangent (arctangent) of `x`, respectively, returning values in radians.
   - `sinh(x)`, `cosh(x)`, `tanh(x)` compute the hyperbolic sine, cosine, and tangent of `x`, respectively.
   - `asinh(x)`, `acosh(x)`, `atanh(x)` compute the inverse hyperbolic sine, cosine, and tangent of `x`, respectively.

5. **Absolute value:**
   - `abs(x)` returns the absolute value of `x`.

6. **Round, Floor, and Ceiling:**
   - `nint(x)` rounds `x` to the nearest integer.
   - `floor(x)` rounds `x` down to the nearest integer.
   - `ceiling(x)` rounds `x` up to the nearest integer.

7. **Modulo:** `mod(a, p)` computes the remainder of `a` divided by `p`.

8. **Maximum and Minimum:**
   - `max(a, b, ...)` returns the maximum of its arguments.
   - `min(a, b, ...)` returns the minimum of its arguments.

Many of these functions are **elemental** and workk both scalars and arrays, computing the function for each element of the array.

It's also important to note that many of these functions come in different versions for different data types.
