Homework6-Exercises
================
Curtis Fox

-   [Writing Functions](#writing-functions)

``` r
options(warn = -1) # supresses warnings
suppressPackageStartupMessages(library(gapminder))
```

``` r
library(gapminder)
```

Writing Functions
-----------------

I'm choosing to do the second option, which is to write some experimental funcations. I'm interested in numerical programming, and so I will write a function that performs gradient descent, and a function that performs Newton's method. Both gradient descent and Newton's method are methods to find the minimum of a function.

Therefore, I first write the function to perform gradient descent:

``` r
# the input parameters are a function f, its derivative df, its second derivative df2, a starting value x0, an accuracy parameter eps, the max number of iterations the while loop can run for maxIter, and a starting stepsize s
gradientDescent = function(f, df, x0, eps, maxIter, s) { 
  i = 0
  x <- x0
  fval <- f(x0)
  dfval <- df(x0)
  while(i < maxIter & dfval > eps){
    x <- x - s * dfval # this step actually performs the descent, to search for the minimization point
    fval <- f(x)
    dfval <- df(x)
    i <- i + 1
  }
  print("x coordinate of minimization point, for gradient descent")
  print(x) # prints the solution, which is the x value of the point that minimizes the function
  print("value of function f at x")
  print(fval) # prints the function value at x
}
```

Now I write a function to perform Newton's method:

``` r
# the input parameters are a function f, its derivative df, its second derivative df2, a starting value x0, an accuracy parameter eps, the max number of iterations the while loop can run for maxIter, and a starting stepsize s
NewtonMethod = function(f, df, df2, x0, eps, maxIter, s) {
  i = 0
  x <- x0
  fval <- f(x0)
  dfval <- df(x0)
  df2val <- df2(x0) # note we need to compute the second derivative for this method
  while(i < maxIter & dfval > eps){
    x <- x - dfval / df2val # note the different descent step compared to gradient descent
    fval <- f(x)
    dfval <- df(x)
    df2val <- df2(x)
    i <- i + 1
  }
  print("x coordinate of minimization point, for Newton's method")
  print(x) # prints the solution, which is the x value of the point that minimizes the function
  print("value of function f at x")
  print(fval) # prints the function value at x
}
```

Note that in general, Newton's method takes fewer iterations of the while loop to find a solution.

I then write an example funcation to pass to gradient descent, in this case the quadratic function x^2.

``` r
f <- function(x) {
  return(x^2)
}
```

I then write a function for the derivative of x^2, which is 2x. The derivative is required for gradient descent method and Newton's method.

``` r
df <- function(x) {
  return(2*x)
}
```

Lastly I write a function for the second derivative of x^2, which is 2. The second derivative is required for Newton's method.

``` r
df2 <- function(x) {
  return(2)
}
```

Note that I wrote functions for the function f, as well as its first and second derivatives. This allows for more robustness, as someone could go in and change these functions withut actually making changes to the gradient descent or newton's method functions.

Now lets actually run gradient descent and Newton's method using our example functions. Note that since these are numerical methods, the solution they give may only be an approximation of the actual solution.

``` r
gradientDescent(f, df, 3, 1e-8, 1000, 0.01)
```

    ## [1] "x coordinate of minimization point, for gradient descent"
    ## [1] 5.048902e-09
    ## [1] "value of function f at x"
    ## [1] 2.549141e-17

``` r
NewtonMethod(f, df, df2, 3, 1e-8, 1000, 0.01)
```

    ## [1] "x coordinate of minimization point, for Newton's method"
    ## [1] 0
    ## [1] "value of function f at x"
    ## [1] 0