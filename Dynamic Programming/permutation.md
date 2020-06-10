``` Written By : DIAO  6/9/20 ```
# Permutation
```
Recursive Formula : 

p(n,k) =   n! if n == k
           n  if k == 1
           p(n-1,k) + k*p(n-1,k-1) else 

```

# Top Down  Approach 
```python
#  k columns , n rows 
def permutation_top(n,k):

	if n < k:
		raise ValueError("not enough n to choose k")
	if n == k:
		return math.factorial(n)
	if k == 1:
		return n
	if k == 0:
		return 1
	
	t = [[None]*(k+1) for _ in range(n+1)]
	return helper(n,k,t)

def helper(n,k,t):
	if t[n][k] != None:
		return t[n][k]

	if k == 1:
		t[n][k] = n
	elif n == k:
		t[n][k] = math.factorial(n)
	else:
		t[n][k] = helper(n-1,k,t) + k*helper(n-1,k-1,t)
	return t[n][k]

```

# Bottom Up Approach 
```python 
#  k columns , n rows 
def permutation_bottom(n,k):
	t = [[0 for i in range(k+1)] for j in range(n+1)] 
	for i in range(1,n+1):
		t[i][1] = i
	for i in range(1,n+1):
		for j in range(2,k+1):
			if i == j:
				t[i][j] = math.factorial(i)
			else:
				t[i][j] = t[i-1][j] + j*t[i-1][j-1]
	return t[i][j]
```