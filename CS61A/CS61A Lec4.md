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

[Python Tutor code visualizer: Visualize code in Python, JavaScript, C, C++, and Java](https://pythontutor.com/visualize.html#code=def%20summation%28n,%20term%29%3A%0A%20%20%20%20total,%20k%20%3D%200,%201%0A%20%20%20%20while%20k%20%3C%3D%20n%3A%0A%20%20%20%20%20%20%20%20total,%20k%20%3D%20total%20%2B%20term%28k%29,%20k%20%2B%201%0A%20%20%20%20return%20total%0A%0Adef%20cube%28x%29%3A%0A%20%20%20%20return%20x*x*x%0A%0Adef%20sum_cubes%28n%29%3A%0A%20%20%20%20return%20summation%28n,%20cube%29%0A%0Aresult%20%3D%20sum_cubes%283%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false)

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

[Python Tutor code visualizer: Visualize code in Python, JavaScript, C, C++, and Java](https://pythontutor.com/visualize.html#code=def%20improve%28update,%20close,%20guess%3D1%29%3A%0A%20%20%20%20while%20not%20close%28guess%29%3A%0A%20%20%20%20%20%20%20%20guess%20%3D%20update%28guess%29%0A%20%20%20%20return%20guess%0A%0Adef%20golden_update%28guess%29%3A%0A%20%20%20%20return%201/guess%20%2B%201%0A%0Adef%20square_close_to_successor%28guess%29%3A%0A%20%20%20%20return%20approx_eq%28guess%20*%20guess,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20guess%20%2B%201%29%0A%0Adef%20approx_eq%28x,%20y,%20tolerance%3D1e-3%29%3A%0A%20%20%20%20return%20abs%28x%20-%20y%29%20%3C%20tolerance%0A%0Aphi%20%3D%20improve%28golden_update,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20square_close_to_successor%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false)

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20improve%28update,%20close,%20guess%3D1%29%3A%0A%20%20%20%20while%20not%20close%28guess%29%3A%0A%20%20%20%20%20%20%20%20guess%20%3D%20update%28guess%29%0A%20%20%20%20return%20guess%0A%0Adef%20golden_update%28guess%29%3A%0A%20%20%20%20return%201/guess%20%2B%201%0A%0Adef%20square_close_to_successor%28guess%29%3A%0A%20%20%20%20return%20approx_eq%28guess%20*%20guess,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20guess%20%2B%201%29%0A%0Adef%20approx_eq%28x,%20y,%20tolerance%3D1e-3%29%3A%0A%20%20%20%20return%20abs%28x%20-%20y%29%20%3C%20tolerance%0A%0Aphi%20%3D%20improve%28golden_update,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20square_close_to_successor%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

## 1.6.3   Defining Functions III: Nested Definitions

**Lexical scope.** Locally defined functions also have access to the name bindings in the scope in which they are defined. In this example, sqrt_update refers to the name a, which is a formal parameter of its enclosing function sqrt. This discipline of sharing names among nested definitions is called _lexical scoping_. Critically, the inner functions have access to the names in the environment where they are defined (not where they are called).

We require two extensions to our environment model to enable lexical scoping.

1.  Each user-defined function has a parent environment: the environment in which it was defined.
2.  When a user-defined function is called, its local frame extends its parent environment.
[Python Tutor code visualizer: Visualize code in Python, JavaScript, C, C++, and Java](https://pythontutor.com/visualize.html#code=def%20average%28x,%20y%29%3A%0A%20%20%20%20return%20%28x%20%2B%20y%29/2%0A%0Adef%20improve%28update,%20close,%20guess%3D1%29%3A%0A%20%20%20%20while%20not%20close%28guess%29%3A%0A%20%20%20%20%20%20%20%20guess%20%3D%20update%28guess%29%0A%20%20%20%20return%20guess%0A%0Adef%20approx_eq%28x,%20y,%20tolerance%3D1e-3%29%3A%0A%20%20%20%20return%20abs%28x%20-%20y%29%20%3C%20tolerance%0A%0Adef%20sqrt%28a%29%3A%0A%20%20%20%20def%20sqrt_update%28x%29%3A%0A%20%20%20%20%20%20%20%20return%20average%28x,%20a/x%29%0A%20%20%20%20def%20sqrt_close%28x%29%3A%0A%20%20%20%20%20%20%20%20return%20approx_eq%28x%20*%20x,%20a%29%0A%20%20%20%20return%20improve%28sqrt_update,%20sqrt_close%29%0A%0Aresult%20%3D%20sqrt%28256%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false)

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

[Python Tutor code visualizer: Visualize code in Python, JavaScript, C, C++, and Java](https://pythontutor.com/visualize.html#code=def%20square%28x%29%3A%0A%20%20%20%20return%20x%20*%20x%0A%0Adef%20successor%28x%29%3A%0A%20%20%20%20return%20x%20%2B%201%0A%0Adef%20compose1%28f,%20g%29%3A%0A%20%20%20%20def%20h%28x%29%3A%0A%20%20%20%20%20%20%20%20return%20f%28g%28x%29%29%0A%20%20%20%20return%20h%0A%0Adef%20f%28x%29%3A%0A%20%20%20%20%22%22%22Never%20called.%22%22%22%0A%20%20%20%20return%20-x%0A%0Asquare_successor%20%3D%20compose1%28square,%20successor%29%0Aresult%20%3D%20square_successor%2812%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false)
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

A motivating comment before we proceed: it is easy to take for granted the fact that we know how to compute square roots. Not just Python, but your phone, web browser, or pocket calculator can do so for you. However, part of learning computer science is understanding how quantities like these can be computed, and the general approach presented here is applicable to solving a large class of equations beyond those built into Python.

Newton's method is an iterative improvement algorithm: it improves a guess of the zero for any function that is _differentiable_, which means that it can be approximated by a straight line at any point. Newton's method follows these linear approximations to find function zeros.

A newton_update expresses the computational process of following this tangent line to 0, for a function f and its derivative df.

```python
>>> def newton_update(f, df):
        def update(x):
            return x - f(x) / df(x)
        return update

```

Finally, we can define the find_root function in terms of newton_update, our improve algorithm, and a comparison to see if f(x) is near 0.

```python

>>> def find_zero(f, df):
        def near_zero(x):
            return approx_eq(f(x), 0)
        return improve(newton_update(f, df), near_zero)
```

## 1.6.6   Currying

We can use higher-order functions to convert a function that takes multiple arguments into a chain of functions that each take a single argument. More specifically, given a function f(x, y), we can define a function g such that g(x)(y) is equivalent to f(x, y). Here, g is a higher-order function that takes in a single argument x and returns another function that takes in a single argument y. This transformation is called _currying_.

As an example, we can define a curried version of the pow function:

```python

>>> def curried_pow(x):
        def h(y):
            return pow(x, y)
        return h

>>> curried_pow(2)(3)
8
```
	for single argument program!

Some programming languages, such as Haskell, only allow functions that take a single argument, so the programmer must curry all multi-argument procedures. In more general languages such as Python, currying is useful when we require a function that takes in only a single argument. For example, the _map_ pattern applies a single-argument function to a sequence of values. In later chapters, we will see more general examples of the map pattern, but for now, we can implement the pattern in a function:

we can define functions to automate currying, as well as the inverse _uncurrying_ transformation:
```python
>>> def curry2(f):
        """Return a curried version of the given two-argument function."""
        def g(x):
            def h(y):
                return f(x, y)
            return h
        return g

>>> def uncurry2(g):
        """Return a two-argument version of the given curried function."""
        def f(x, y):
            return g(x)(y)
        return f

>>> pow_curried = curry2(pow)
>>> pow_curried(2)(5)
32
>>> map_to_range(0, 10, pow_curried(2))
1
2
4
8
16
32
64
128
256
512
```

The curry2 function takes in a two-argument function f and returns a single-argument function g. When g is applied to an argument x, it returns a single-argument function h. When h is applied to y, it calls f(x, y). Thus, curry2(f)(x)(y) is equivalent to f(x, y). The uncurry2 function reverses the currying transformation, so that uncurry2(curry2(f)) is equivalent to f.

```python
>>> uncurry2(pow_curried)(2, 5)
32
```
## 1.6.7   Lambda Expressions

So far, each time we have wanted to define a new function, we needed to give it a name. But for other types of expressions, we don't need to associate intermediate values with a name. That is, we can compute a*b + c*d without having to name the subexpressions a*b or c*d, or the full expression. In Python, we can create function values on the fly using lambda expressions, which evaluate to unnamed functions. A lambda expression evaluates to a function that has a single return expression as its body. Assignment and control statements are not allowed.

到目前为止，每当我们想要定义一个新函数时，都需要给它取一个名字。但是对于其他类型的表达式，我们不需要将中间值与名称相关联。也就是说，我们可以计算 `a * b + c * d` 而不必命名子表达式 `a*b` 或 `c*d` 或完整的表达式。


```python
>>> def compose1(f, g):
        return lambda x: f(g(x))
```

We can understand the structure of a lambda expression by constructing a corresponding English sentence:

```python
 lambda            x            :          f(g(x))
"A function that    takes x    and returns     f(g(x))"
```


	The result of a lambda expression is called a lambda function. It has no intrinsic name (and so Python prints <lambda> for the name), but otherwise it behaves like any other function.

```python
>>> s = lambda x: x * x
>>> s
<function <lambda> at 0xf3f490>
>>> s(12)
144
```
In an environment diagram, the result of a lambda expression is a function as well, named with the greek letter λ (lambda). Our compose example can be expressed quite compactly with lambda expressions.

[Python Tutor code visualizer: Visualize code in Python, JavaScript, C, C++, and Java](https://pythontutor.com/visualize.html#code=def%20compose1%28f,%20g%29%3A%0A%20%20%20%20return%20lambda%20x%3A%20f%28g%28x%29%29%0A%0Af%20%3D%20compose1%28lambda%20x%3A%20x%20*%20x,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20lambda%20y%3A%20y%20%2B%201%29%0Aresult%20%3D%20f%2812%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false)

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20compose1%28f,%20g%29%3A%0A%20%20%20%20return%20lambda%20x%3A%20f%28g%28x%29%29%0A%0Af%20%3D%20compose1%28lambda%20x%3A%20x%20*%20x,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20lambda%20y%3A%20y%20%2B%201%29%0Aresult%20%3D%20f%2812%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

## 1.6.8   Abstractions and First-Class Functions

Some of the "rights and privileges" of first-class elements are:

1.  They may be bound to names.
2.  They may be passed as arguments to functions.
3.  They may be returned as the results of functions.
4.  They may be included in data structures.

Python awards functions full first-class status, and the resulting gain in expressive power is enormous.

## 1.6.9   Function Decorators

Python provides special syntax to apply higher-order functions as part of executing a def statement, called a decorator. Perhaps the most common example is a trace.

```python
>>> def trace(fn):
        def wrapped(x):
            print('-> ', fn, '(', x, ')')
            return fn(x)
        return wrapped

>>> @trace
    def triple(x):
        return 3 * x

>>> triple(12)
->  <function triple at 0x102a39848> ( 12 )
36
```

In this example, A higher-order function trace is defined, which returns a function that precedes a call to its argument with a print statement that outputs the argument. The def statement for triple has an annotation, @trace, which affects the execution rule for def. As usual, the function triple is created. However, the name triple is not bound to this function. Instead, the name triple is bound to the returned function value of calling trace on the newly defined triple function. In code, this decorator is equivalent to:

```python
>>> def triple(x):
        return 3 * x

>>> triple = trace(triple)
```


In the projects associated with this text, decorators are used for tracing, as well as selecting which functions to call when a program is run from the command line.

**Extra for experts.** The decorator symbol @ may also be followed by a call expression. The expression following @ is evaluated first (just as the name trace was evaluated above), the def statement second, and finally the result of evaluating the decorator expression is applied to the newly defined function, and the result is bound to the name in the def statement. A [short tutorial on decorators](http://programmingbits.pythonblogs.com/27_programmingbits/archive/50_function_decorators.html) by Ariel Ortiz gives further examples for interested students.