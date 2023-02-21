# 1.3 How to define a new function：
1. def statement
2. indicates a <name>
3. a comma-separated list of named <formal parameters>
4.  a return statement
5. called the function body：specifies the <return expression> of the function
	```python
	def <name>(<formal parameters>):
		return <return expression>
	```
6. The second line _must_ be indented — most programmers use four spaces to indent

## 1.3.1 Environments
https://pythontutor.com/cp/composingprograms.html#mode=display

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=from%20math%20import%20pi%0Atau%20%3D%202%20*%20pi&codeDivHeight=400&codeDivWidth=350&cumulative=true&curInstr=2&origin=composingprograms.js&py=3&rawInputLstJSON=%5B%5D"> </iframe>

https://pythontutor.com/cp/composingprograms.html#code=from%20operator%20import%20mul%0Adef%20square%28x%29%3A%0A%20%20%20%20return%20mul%28x,%20x%29&cumulative=true&curInstr=0&mode=display&origin=composingprograms.js&py=3&rawInputLstJSON=%5B%5D

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=from%20operator%20import%20mul%0Adef%20square%28x%29%3A%0A%20%20%20%20return%20mul%28x,%20x%29&codeDivHeight=400&codeDivWidth=350&cumulative=true&curInstr=2&origin=composingprograms.js&py=3&rawInputLstJSON=%5B%5D"> </iframe>


	The name appearing in the function is called the _intrinsic name_. The name in a frame is a _bound name_. There is a difference between the two: different names may refer to the same function, but that function itself has only one **intrinsic name**.

https://pythontutor.com/cp/composingprograms.html#code=f%20%3D%20max%0Amax%20%3D%203%0Aresult%20%3D%20f%282,%203,%204%29%0Amax%281,%202%29%20%23%20cause%20an%20error&cumulative=true&curInstr=4&mode=display&origin=composingprograms.js&py=3&rawInputLstJSON=%5B%5D

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=f%20%3D%20max%0Amax%20%3D%203%0Aresult%20%3D%20f%282,%203,%204%29%0Amax%281,%202%29%20%23%20cause%20an%20error&codeDivHeight=400&codeDivWidth=350&cumulative=true&curInstr=4&origin=composingprograms.js&py=3&rawInputLstJSON=%5B%5D"> </iframe>

## 1.3.2   Calling User-Defined Functions
https://pythontutor.com/cp/composingprograms.html#code=from%20operator%20import%20mul%0Adef%20square%28x%29%3A%0A%20%20%20%20return%20mul%28x,%20x%29%0Asquare%28-2%29&cumulative=true&curInstr=6&mode=display&origin=composingprograms.js&py=3&rawInputLstJSON=%5B%5D

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=from%20operator%20import%20mul%0Adef%20square%28x%29%3A%0A%20%20%20%20return%20mul%28x,%20x%29%0Asquare%28-2%29&codeDivHeight=400&codeDivWidth=350&cumulative=true&curInstr=6&origin=composingprograms.js&py=3&rawInputLstJSON=%5B%5D"> </iframe>

## 1.3.3   Example: Calling a User-Defined Function
https://pythontutor.com/cp/composingprograms.html#code=from%20operator%20import%20add,mul%0Adef%20square%28x%29%3A%0A%20%20%20%20return%20mul%28x,%20x%29%0A%0Adef%20sum_square%28x,%20y%29%3A%0A%20%20%20%20return%20add%28square%28x%29,%20suqare%28y%29%29%0A%20%20%20%20%0A%20%20%20%20%0Aresult%20%3D%20sum_square%285,%2012%29&cumulative=true&curInstr=11&mode=display&origin=composingprograms.js&py=3&rawInputLstJSON=%5B%5D

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=from%20operator%20import%20add,mul%0Adef%20square%28x%29%3A%0A%20%20%20%20return%20mul%28x,%20x%29%0A%0Adef%20sum_square%28x,%20y%29%3A%0A%20%20%20%20return%20add%28square%28x%29,%20suqare%28y%29%29%0A%20%20%20%20%0A%20%20%20%20%0Aresult%20%3D%20sum_square%285,%2012%29&codeDivHeight=400&codeDivWidth=350&cumulative=true&curInstr=11&origin=composingprograms.js&py=3&rawInputLstJSON=%5B%5D"> </iframe>


## 1.3.4   Local Names
函数的形参选择的名称不应该影响函数行为

```python
>>> def square(x):
        return mul(x, x)
>>> def square(y):
        return mul(y, y)
```


## 1.3.5   Choosing Names
The following guidelines are adapted from the [style guide for Python code](http://www.python.org/dev/peps/pep-0008), which serves as a guide for all (non-rebellious) Python programmers. A shared set of conventions smooths communication among members of a developer community. As a side effect of following these conventions, you will find that your code becomes more internally consistent.

1.  Function names are lowercase, with words separated by underscores. Descriptive names are encouraged.
2.  Function names typically evoke operations applied to arguments by the interpreter (e.g., print, add, square) or the name of the quantity that results (e.g., max, abs, sum).
3.  Parameter names are lowercase, with words separated by underscores. Single-word names are preferred.
4.  Parameter names should evoke the role of the parameter in the function, not just the kind of argument that is allowed.
5.  Single letter parameter names are acceptable when their role is obvious, but avoid "l" (lowercase ell), "O" (capital oh), or "I" (capital i) to avoid confusion with numerals.

## 1.3.6   Functions as Abstractions
**Aspects of a functional abstraction.** To master the use of a functional abstraction, it is often useful to consider its three core attributes. The _domain_ of a function is the set of arguments it can take. The _range_ of a function is the set of values it can return. The _intent_ of a function is the relationship it computes between inputs and output (as well as any side effects it might generate). Understanding functional abstractions via their domain, range, and intent is critical to using them correctly in a complex program.
For example, any square function that we use to implement sum_squares should have these attributes:

-   The _domain_ is any single real number.
-   The _range_ is any non-negative real number.
-   The _intent_ is that the output is the square of the input.

## 1.3.7   Operators
When it comes to division, Python provides two infix operators: / and //. The former is normal division, so that it results in a _floating point_, or decimal value, even if the divisor evenly divides the dividend:

```python
>>> 5 / 4
1.25
>>> 8 / 4
2.0
```

The // operator, on the other hand, rounds the result down to an integer:

```python
>>> 5 // 4
1
>>> -5 // 4
-2
```


These two operators are shorthand for the truediv and floordiv functions.


```python
>>> from operator import truediv, floordiv
>>> truediv(5, 4)
1.25
>>> floordiv(5, 4)
1
```

You should feel free to use infix operators and parentheses in your programs. Idiomatic Python prefers operators over call expressions for simple mathematical operations.

