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

