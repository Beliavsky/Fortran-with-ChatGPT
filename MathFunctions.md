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

Many of these functions are **elemental** and work both scalars and arrays, computing the function for each element of the array.

It's also important to note that many of these functions come in different versions for different data types.

---
**What intrinsic math functions were added to Fortran 2008?**

Fortran 2008 introduced several new intrinsic math functions. Some of the notable additions include:

1. `acosh(x)`: Returns the inverse hyperbolic cosine of `x`.
2. `asinh(x)`: Returns the inverse hyperbolic sine of `x`.
3. `atanh(x)`: Returns the inverse hyperbolic tangent of `x`.
4. `bessel_j0(x)`: Returns the Bessel function of the first kind of order zero evaluated at `x`.
5. `bessel_j1(x)`: Returns the Bessel function of the first kind of order one evaluated at `x`.
6. `bessel_jn(n, x)`: Returns the Bessel function of the first kind of order `n` evaluated at `x`.
7. `bessel_y0(x)`: Returns the Bessel function of the second kind of order zero evaluated at `x`.
8. `bessel_y1(x)`: Returns the Bessel function of the second kind of order one evaluated at `x`.
9. `bessel_yn(n, x)`: Returns the Bessel function of the second kind of order `n` evaluated at `x`.
10. `erfc(x)`: Returns the complementary error function of `x`.
11. `erfc_scaled(x)`: Returns the scaled complementary error function of `x`.
12. `erfcx(x)`: Returns the scaled complementary error function of `x`.
13. `gamma(x)`: Returns the gamma function of `x`.
14. `log_gamma(x)`: Returns the natural logarithm of the absolute value of the gamma function of `x`.

These are just some of the new intrinsic math functions added in Fortran 2008. The complete list can be found in the Fortran 2008 standard documentation. **Note:** the functions are detailed in the [gfortran documentation](https://gcc.gnu.org/onlinedocs/gfortran/Intrinsic-Procedures.html).
