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
