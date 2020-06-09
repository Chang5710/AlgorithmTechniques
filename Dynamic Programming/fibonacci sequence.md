``` Written By : DIAO  6/8/20 ```
# Fibonacci sequence is a sequence of numbers where each element is composed from adding the previous two element.
```
Recursive Formula : 

fib(n) = 0 if n=0 
		 1 if n=1 
		 fib(n-1) + fib(n-2) else


```

# Top Down  Approach 
```python

def fib_top(n):
	t = [-1]*(n+1)
	t[0] = 0
	t[1] = 1
	return fib(n,t)

def fib(n,t):
	if t[n] >= 0:
		return t[n]
	res = fib(n-1,t)+fib(n-2,t)
	t[n] = res
	return res

```

# Bottom Up Approach 
```python 
def fib_bottom(n):
	t = [0]*(n+1)
	t[1] = 1 
	for i in range(2,n+1):
		t[i] = t[i-1]+t[i-2]
	return t[n]

```