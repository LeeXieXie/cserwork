
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

# 1.4  Designing Functions
Fundamentally, the qualities of good functions all reinforce the idea that functions are abstractions.

-   Each function should have exactly one job. That job should be identifiable with a short name and characterizable in a single line of text. Functions that perform multiple jobs in sequence should be divided into multiple functions.
-   _Don't repeat yourself_ is a central tenet of software engineering. The so-called DRY principle states that multiple fragments of code should not describe redundant logic. Instead, that logic should be implemented once, given a name, and applied multiple times. If you find yourself copying and pasting a block of code, you have probably found an opportunity for functional abstraction.
-   Functions should be defined generally. Squaring is not in the Python Library precisely because it is a special case of the pow function, which raises numbers to arbitrary powers.

## 1.4.1   Documentation
A function definition will often include documentation describing the function, called a _docstring_, which must be indented along with the function body. Docstrings are conventionally triple quoted. The first line describes the job of the function in one line. The following lines can describe arguments and clarify the behavior of the function:


```python
>>> def pressure(v, t, n):
        """Compute the pressure in pascals of an ideal gas.

        Applies the ideal gas law: http://en.wikipedia.org/wiki/Ideal_gas_law

        v -- volume of gas, in cubic meters
        t -- absolute temperature in degrees kelvin
        n -- particles of gas
        """
        k = 1.38e-23  # Boltzmann's constant
        return n * k * t / v
```

When you call help with the name of a function as an argument, you see its docstring (type q to quit Python help).


```python
>>> help(pressure)
```

**Comments**. Comments in Python can be attached to the end of a line following the # symbol. For example, the comment Boltzmann's constant above describes k. These comments don't ever appear in Python's help, and they are ignored by the interpreter. They exist for humans alone.

As a guideline, most data values used in a function's body should be expressed as default values to named arguments, so that they are easy to inspect and can be changed by the function caller. Some values that never change, such as the fundamental constant k, can be bound in the function body or in the global frame.

# 1.5 Control

## 1.5.2   Compound Statements
A simple statement is a single line that doesn't end in a colon;
Compound statements typically span multiple lines and start with a one-line header ending in a colon;

 A compound statement consists of one or more clauses:
```python
<header>:
    <statement>
    <statement>
    ...
<separating header>:
    <statement>
    <statement>
    ...
...
```
We can understand the statements we have already introduced in these terms.

-   Expressions, return statements, and assignment statements are simple statements.
-   A def statement is a compound statement. The suite that follows the def header defines the function body.

We can also understand multi-line programs now.

-   To execute a sequence of statements, execute the first statement. If that statement does not redirect control, then proceed to execute the rest of the sequence of statements, if any remain.

**Practical Guidance.** When indenting a suite, all lines must be indented the same amount and in the same way (use spaces, not tabs). Any variation in indentation will cause an error.

## 1.5.3   Defining Functions II: Local Assignment
https://pythontutor.com/cp/composingprograms.html#code=def%20percent_difference%28x,%20y%29%3A%0A%20%20%20%20difference%20%3D%20abs%28x-y%29%0A%20%20%20%20return%20100%20*%20difference%20/%20x%0Aresult%20%3D%20percent_difference%2840,%2050%29&cumulative=true&curInstr=6&mode=display&origin=composingprograms.js&py=3&rawInputLstJSON=%5B%5D

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20percent_difference%28x,%20y%29%3A%0A%20%20%20%20difference%20%3D%20abs%28x-y%29%0A%20%20%20%20return%20100%20*%20difference%20/%20x%0Aresult%20%3D%20percent_difference%2840,%2050%29&codeDivHeight=400&codeDivWidth=350&cumulative=true&curInstr=6&origin=composingprograms.js&py=3&rawInputLstJSON=%5B%5D"> </iframe>

## 1.5.4   Conditional Statements
**Conditional statements**. A conditional statement in Python consists of a series of headers and suites: a required if clause, an optional sequence of elif clauses, and finally an optional else clause:

```python
if <expression>:
    <suite>
elif <expression>:
    <suite>
else:
    <suite>
```
When executing a conditional statement, each clause is considered in order. The computational process of executing a conditional clause follows.

1.  Evaluate the header's expression.
2.  If it is a true value, execute the suite. Then, skip over all subsequent clauses in the conditional statement.

If the else clause is reached (which only happens if all if and elif expressions evaluate to false values), its suite is executed.

**Boolean contexts**. Above, the execution procedures mention "a false value" and "a true value." The expressions inside the header statements of conditional blocks are said to be in _boolean contexts_: their truth values matter to control flow, but otherwise their values are not assigned or returned. Python includes several false values, including 0, None, and the _boolean_ value False. All other numbers are true values.

**Boolean values**. Python has two boolean values, called True and False. Boolean values represent truth values in logical expressions. The built-in comparison operations, >, <, >=, <=, ==, !=, return these values.

```python
>>> 4 < 2
False
>>> 5 >= 5
True
```


This second example reads "5 is greater than or equal to 5", and corresponds to the function ge in the operator module.

```python
>>> 0 == -0
True
```



This final example reads "0 equals -0", and corresponds to eq in the operator module. Notice that Python distinguishes assignment (=) from equality comparison (==), a convention shared across many programming languages.

**Boolean operators**. Three basic logical operators are also built into Python:


```python

>>> True and False
False
>>> True or False
True
>>> not False
True

```

Logical expressions have corresponding evaluation procedures. These procedures exploit the fact that the truth value of a logical expression can sometimes be determined without evaluating all of its subexpressions, a feature called _short-circuiting_.

To evaluate the expression `< left >` and `< right >`:

1.  Evaluate the subexpression `< left >`.
2.  If the result is a false value v, then the expression evaluates to v.
3.  Otherwise, the expression evaluates to the value of the subexpression < right >.

To evaluate the expression < left > or < right >:

1.  Evaluate the subexpression < left >.
2.  If the result is a true value v, then the expression evaluates to v.
3.  Otherwise, the expression evaluates to the value of the subexpression < right >.

To evaluate the expression not < exp >:

1.  Evaluate < exp >; The value is True if the result is a false value, and False otherwise.

These values, rules, and operators provide us with a way to combine the results of comparisons. Functions that perform comparisons and return boolean values typically begin with is, not followed by an underscore (e.g., isfinite, isdigit, isinstance, etc.).

## 1.5.5   Iteration


## 1.5.6   Testing

_Testing_ a function is the act of verifying that the function's behavior matches expectations. Our language of functions is now sufficiently complex that we need to start testing our implementations.

A _test_ is a mechanism for systematically performing this verification. Tests typically take the form of another function that contains one or more sample calls to the function being tested. The returned value is then verified against an expected result. Unlike most functions, which are meant to be general, tests involve selecting and validating calls with specific argument values. Tests also serve as documentation: they demonstrate how to call a function and what argument values are appropriate.

**Assertions.** Programmers use assert statements to verify expectations, such as the output of a function being tested. An assert statement has an expression in a boolean context, followed by a quoted line of text (single or double quotes are both fine, but be consistent) that will be displayed if the expression evaluates to a false value.


```python
>>> assert fib(8) == 13, 'The 8th Fibonacci number should be 13'

```
When the expression being asserted evaluates to a true value, executing an assert statement has no effect. When it is a false value, assert causes an error that halts execution.

A test function for fib should test several arguments, including extreme values of n.


```python
>>> def fib_test():
        assert fib(2) == 1, 'The 2nd Fibonacci number should be 1'
        assert fib(3) == 1, 'The 3rd Fibonacci number should be 1'
        assert fib(50) == 7778742049, 'Error at the 50th Fibonacci number'
```


When writing Python in files, rather than directly into the interpreter, tests are typically written in the same file or a neighboring file with the suffix _test.py.

**Doctests.** Python provides a convenient method for placing simple tests directly in the docstring of a function. The first line of a docstring should contain a one-line description of the function, followed by a blank line. A detailed description of arguments and behavior may follow. In addition, the docstring may include a sample interactive session that calls the function:

```python
>>> def sum_naturals(n):
        """Return the sum of the first n natural numbers.

        >>> sum_naturals(10)
        55
        >>> sum_naturals(100)
        5050
        """
        total, k = 0, 1
        while k <= n:
            total, k = total + k, k + 1
        return total
```

Then, the interaction can be verified via the [doctest module](http://docs.python.org/py3k/library/doctest.html). Below, the globals function returns a representation of the global environment, which the interpreter needs in order to evaluate expressions.



```python
>>> from doctest import testmod
>>> testmod()
TestResults(failed=0, attempted=2)
```


To verify the doctest interactions for only a single function, we use a doctest function called run_docstring_examples. This function is (unfortunately) a bit complicated to call. Its first argument is the function to test. The second should always be the result of the expression globals(), a built-in function that returns the global environment. The third argument is True to indicate that we would like "verbose" output: a catalog of all tests run.

```python
>>> from doctest import run_docstring_examples
>>> run_docstring_examples(sum_naturals, globals(), True)
Finding tests in NoName
Trying:
    sum_naturals(10)
Expecting:
    55
ok
Trying:
    sum_naturals(100)
Expecting:
    5050
ok

```



When the return value of a function does not match the expected result, the run_docstring_examples function will report this problem as a test failure.

When writing Python in files, all doctests in a file can be run by starting Python with the doctest command line option:


```python
python3 -m doctest <python_source_file>
```


The key to effective testing is to write (and run) tests immediately after implementing new functions. It is even good practice to write some tests before you implement, in order to have some example inputs and outputs in your mind. A test that applies a single function is called a _unit test_. Exhaustive unit testing is a hallmark of good program design.



![](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202302230028687.png)

![](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202302230028687.png)