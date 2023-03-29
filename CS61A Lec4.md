# 1.6   Higher-Order Functions
This section shows how higher-order functions can serve as powerful abstraction mechanisms, vastly increasing the expressive power of our language.
## 1.6.1   Functions as Arguments
a common underlying pattern
```python
def <name>(n):
    total, k = 0, 1
    while k <= n:
        total, k = total + <term>(k), k + 1
    return total
```

https://pythontutor.com/visualize.html#code=def%20summation%28n,%20term%29%3A%0A%20%20%20%20total,%20k%20%3D%200,%201%0A%20%20%20%20while%20k%20%3C%3D%20n%3A%0A%20%20%20%20%20%20%20%20total,%20k%20%3D%20total%20%2B%20term%28k%29,%20k%20%2B%201%0A%20%20%20%20return%20total%0A%0Adef%20cube%28x%29%3A%0A%20%20%20%20return%20x*x*x%0A%0Adef%20sum_cubes%28n%29%3A%0A%20%20%20%20return%20summation%28n,%20cube%29%0A%0Aresult%20%3D%20sum_cubes%283%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20summation%28n,%20term%29%3A%0A%20%20%20%20total,%20k%20%3D%200,%201%0A%20%20%20%20while%20k%20%3C%3D%20n%3A%0A%20%20%20%20%20%20%20%20total,%20k%20%3D%20total%20%2B%20term%28k%29,%20k%20%2B%201%0A%20%20%20%20return%20total%0A%0Adef%20cube%28x%29%3A%0A%20%20%20%20return%20x*x*x%0A%0Adef%20sum_cubes%28n%29%3A%0A%20%20%20%20return%20summation%28n,%20cube%29%0A%0Aresult%20%3D%20sum_cubes%283%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Using an identity function that returns its argument, we can also sum natural numbers using exactly the same summation function.

```python
	>>> def summation(n, term):
        total, k = 0, 1
        while k <= n:
            total, k = total + term(k), k + 1
        return total
    >>> def identity(x):
        return x
    >>> def sum_naturals(n):
        return summation(n, identity)
    >>> sum_naturals(10)
    55
```

## 1.6.2   Functions as General Methods
 With higher-order functions, we begin to see a more powerful kind of abstraction: some functions express general methods of computation, independent of the particular functions they call.

https://pythontutor.com/visualize.html#code=def%20improve%28update,%20close,%20guess%3D1%29%3A%0A%20%20%20%20while%20not%20close%28guess%29%3A%0A%20%20%20%20%20%20%20%20guess%20%3D%20update%28guess%29%0A%20%20%20%20return%20guess%0A%0Adef%20golden_update%28guess%29%3A%0A%20%20%20%20return%201/guess%20%2B%201%0A%0Adef%20square_close_to_successor%28guess%29%3A%0A%20%20%20%20return%20approx_eq%28guess%20*%20guess,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20guess%20%2B%201%29%0A%0Adef%20approx_eq%28x,%20y,%20tolerance%3D1e-3%29%3A%0A%20%20%20%20return%20abs%28x%20-%20y%29%20%3C%20tolerance%0A%0Aphi%20%3D%20improve%28golden_update,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20square_close_to_successor%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20improve%28update,%20close,%20guess%3D1%29%3A%0A%20%20%20%20while%20not%20close%28guess%29%3A%0A%20%20%20%20%20%20%20%20guess%20%3D%20update%28guess%29%0A%20%20%20%20return%20guess%0A%0Adef%20golden_update%28guess%29%3A%0A%20%20%20%20return%201/guess%20%2B%201%0A%0Adef%20square_close_to_successor%28guess%29%3A%0A%20%20%20%20return%20approx_eq%28guess%20*%20guess,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20guess%20%2B%201%29%0A%0Adef%20approx_eq%28x,%20y,%20tolerance%3D1e-3%29%3A%0A%20%20%20%20return%20abs%28x%20-%20y%29%20%3C%20tolerance%0A%0Aphi%20%3D%20improve%28golden_update,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20square_close_to_successor%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

## 1.6.3   Defining Functions III: Nested Definitions

**Lexical scope.** Locally defined functions also have access to the name bindings in the scope in which they are defined. In this example, sqrt_update refers to the name a, which is a formal parameter of its enclosing function sqrt. This discipline of sharing names among nested definitions is called _lexical scoping_. Critically, the inner functions have access to the names in the environment where they are defined (not where they are called).

We require two extensions to our environment model to enable lexical scoping.

1.  Each user-defined function has a parent environment: the environment in which it was defined.
2.  When a user-defined function is called, its local frame extends its parent environment.
https://pythontutor.com/visualize.html#code=def%20average%28x,%20y%29%3A%0A%20%20%20%20return%20%28x%20%2B%20y%29/2%0A%0Adef%20improve%28update,%20close,%20guess%3D1%29%3A%0A%20%20%20%20while%20not%20close%28guess%29%3A%0A%20%20%20%20%20%20%20%20guess%20%3D%20update%28guess%29%0A%20%20%20%20return%20guess%0A%0Adef%20approx_eq%28x,%20y,%20tolerance%3D1e-3%29%3A%0A%20%20%20%20return%20abs%28x%20-%20y%29%20%3C%20tolerance%0A%0Adef%20sqrt%28a%29%3A%0A%20%20%20%20def%20sqrt_update%28x%29%3A%0A%20%20%20%20%20%20%20%20return%20average%28x,%20a/x%29%0A%20%20%20%20def%20sqrt_close%28x%29%3A%0A%20%20%20%20%20%20%20%20return%20approx_eq%28x%20*%20x,%20a%29%0A%20%20%20%20return%20improve%28sqrt_update,%20sqrt_close%29%0A%0Aresult%20%3D%20sqrt%28256%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20average%28x,%20y%29%3A%0A%20%20%20%20return%20%28x%20%2B%20y%29/2%0A%0Adef%20improve%28update,%20close,%20guess%3D1%29%3A%0A%20%20%20%20while%20not%20close%28guess%29%3A%0A%20%20%20%20%20%20%20%20guess%20%3D%20update%28guess%29%0A%20%20%20%20return%20guess%0A%0Adef%20approx_eq%28x,%20y,%20tolerance%3D1e-3%29%3A%0A%20%20%20%20return%20abs%28x%20-%20y%29%20%3C%20tolerance%0A%0Adef%20sqrt%28a%29%3A%0A%20%20%20%20def%20sqrt_update%28x%29%3A%0A%20%20%20%20%20%20%20%20return%20average%28x,%20a/x%29%0A%20%20%20%20def%20sqrt_close%28x%29%3A%0A%20%20%20%20%20%20%20%20return%20approx_eq%28x%20*%20x,%20a%29%0A%20%20%20%20return%20improve%28sqrt_update,%20sqrt_close%29%0A%0Aresult%20%3D%20sqrt%28256%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>



Function values each have a new annotation that we will include in environment diagrams from now on, a _parent_. The parent of a function value is the first frame of the environment in which that function was defined. Functions without parent annotations were defined in the global environment. When a user-defined function is called, the frame created has the same parent as that function.

Subsequently, the name sqrt_update resolves to this newly defined function, which is passed as an argument to improve. Within the body of improve, we must apply our update function (bound to sqrt_update) to the initial guess x of 1. This final application creates an environment for sqrt_update that begins with a local frame containing only x, but with the parent frame sqrt still containing a binding for a.

**Extended Environments**. An environment can consist of an arbitrarily long chain of frames, which always concludes with the global frame. Previous to this sqrt example, environments had at most two frames: a local frame and the global frame. By calling functions that were defined within other functions, via nested def statements, we can create longer chains. The environment for this call to sqrt_update consists of three frames: the local sqrt_update frame, the sqrt frame in which sqrt_update was defined (labeled f1), and the global frame.

The return expression in the body of sqrt_update can resolve a value for a by following this chain of frames. Looking up a name finds the first value bound to that name in the current environment. Python checks first in the sqrt_update frame -- no a exists. Python checks next in the parent frame, f1, and finds a binding for a to 256.

Hence, we realize two key advantages of lexical scoping in Python.

-   The names of a local function do not interfere with names external to the function in which it is defined, because the local function name will be bound in the current local environment in which it was defined, rather than the global environment.
-   A local function can access the environment of the enclosing function, because the body of the local function is evaluated in an environment that extends the evaluation environment in which it was defined.

The sqrt_update function carries with it some data: the value for a referenced in the environment in which it was defined. Because they "enclose" information in this way, locally defined functions are often called _closures_(闭包).

## 1.6.4   Functions as Returned Values
We can achieve even more expressive power in our programs by creating functions whose returned values are themselves functions. An important feature of lexically scoped programming languages is that locally defined functions maintain their parent environment when they are returned. The following example illustrates the utility of this feature.

Once many simple functions are defined, function _composition_ is a natural method of combination to include in our programming language. That is, given two functions f(x) and g(x), we might want to define h(x) = f(g(x)). We can define function composition using our existing tools:

```python
>>> def compose1(f, g):
        def h(x):
            return f(g(x))
        return h 
>>> define h(x) = f(g(x))
```

https://pythontutor.com/visualize.html#code=def%20square%28x%29%3A%0A%20%20%20%20return%20x%20*%20x%0A%0Adef%20successor%28x%29%3A%0A%20%20%20%20return%20x%20%2B%201%0A%0Adef%20compose1%28f,%20g%29%3A%0A%20%20%20%20def%20h%28x%29%3A%0A%20%20%20%20%20%20%20%20return%20f%28g%28x%29%29%0A%20%20%20%20return%20h%0A%0Adef%20f%28x%29%3A%0A%20%20%20%20%22%22%22Never%20called.%22%22%22%0A%20%20%20%20return%20-x%0A%0Asquare_successor%20%3D%20compose1%28square,%20successor%29%0Aresult%20%3D%20square_successor%2812%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false
<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20square%28x%29%3A%0A%20%20%20%20return%20x%20*%20x%0A%0Adef%20successor%28x%29%3A%0A%20%20%20%20return%20x%20%2B%201%0A%0Adef%20compose1%28f,%20g%29%3A%0A%20%20%20%20def%20h%28x%29%3A%0A%20%20%20%20%20%20%20%20return%20f%28g%28x%29%29%0A%20%20%20%20return%20h%0A%0Adef%20f%28x%29%3A%0A%20%20%20%20%22%22%22Never%20called.%22%22%22%0A%20%20%20%20return%20-x%0A%0Asquare_successor%20%3D%20compose1%28square,%20successor%29%0Aresult%20%3D%20square_successor%2812%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>
The 1 in compose1 is meant to signify that the composed functions all take a single argument. This naming convention is not enforced by the interpreter; the 1 is just part of the function name.
	(`compose1` 中的 1 表示这个组合的函数只有一个参数。这个命名惯例不是解释器强制要求的，1 只是函数名的一部分而已。)

## 1.6.5   Example: Newton's Method

> Newton's Method is a numerical method used to find the roots of a function. It is based on the idea of using the tangent line to a curve to approximate the location of its roots. The method starts with an initial guess for the root of the function and then uses the tangent line to the curve at that point to find a better approximation for the root. This process is repeated until the desired level of accuracy is achieved.
> 
> The formula for Newton's Method is:
> 
> x_{n+1} = x_n - f(x_n) / f'(x_n)
> 
> where x_n is the nth approximation for the root, f(x_n) is the value of the function at x_n, and f'(x_n) is the derivative of the function at x_n.
> 
> The method can be used to find both real and complex roots of a function. However, it may not converge to a root if the initial guess is too far from the actual root or if the function has multiple roots in the same vicinity.
> 
> Newton's Method is widely used in various fields such as engineering, physics, and finance for solving complex problems that involve finding the roots of a function.

