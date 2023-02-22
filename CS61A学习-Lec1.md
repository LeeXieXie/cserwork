## python
### 1.Objects

```python
text[:25] #从第0位（包括）截取到第25位（不包括）
text[:-1] #从第0位（包括）截取到倒数第1位（不包括）
'draw'[::-1] #倒序输出
```
![从第2位开始（包含）截取到第7位（不包含）](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202301081200549.png)

b = a[i:j]   表示复制 a[i] 到 a[j-1]，以生成新的 list 对象

a = [0,1,2,3,4,5,6,7,8,9]  
b = a[1:3]   # [1,2]  
当 i 缺省时，默认为 0，即 a[:3] 相当于 a[0:3]  
当 j 缺省时，默认为 len(alist), 即 a[1:] 相当于 a[1:10]  
当 i,j 都缺省时，a[:] 就相当于完整复制一份 a

b = a[i:j:s] 表示：i,j 与上面的一样，但 s 表示步进，缺省为 1.  
所以 a[i:j:1] 相当于 a[i:j]  
当 s<0 时，i 缺省时，默认为 - 1. j 缺省时，默认为 - len(a)-1  
所以 a[::-1] 相当于 a[-1:-len(a)-1:-1]，也就是从最后一个元素到第一个元素复制一遍，即倒序。

### 2.集合解析式

注意一个概念，集合是不可重复的，集合解析式能够自动实现去重功能。其实这里的用法和上述的字典有点相似，仔细看清楚哦。

*   基本语法格式：{expression for i in iterable}
*   用法和字典类似，也是用 { } 包起来，但是前面的 expression 不再是 key:value 的形式。

```python
x = ["香蕉","橘子","西瓜","香蕉","橘子"]
y = {i for i in x}
print(y)
```

结果如下：  
![image.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202301081705794.png)
```Python
{w[0] for w in words}
{w for w in words if w == w[::-1] and len(w) > 4}
{w for w in words if w == w[::-1] and len(w) == 4}
{w for w in words if w == w[::-1] and len(w) > 6}
```


1 + 1