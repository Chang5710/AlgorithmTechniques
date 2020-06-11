``` Written By : DIAO  6/10/20 ```
# Rod Cut 
### Given a rod of length n inches and a table of prices p_i for i = 1,2 ... , n. Determine the maximum revenue r_n obtainable by cutting up the rod and selling the pieces. 
```
Recursive Formula : 

r(n) = max(p_i + r(n-1)) for 1 <= i <= n

```

# Top Down  Approach 
```python
#  k columns , n rows 
def memoized_cut_rod(p,n):
	r = [-1] * (n+1)
	return memoized_cut_rod_helper(p,n,r)

def memoized_cut_rod_helper(p,n,r):
	if r[n] >= 0:
		return r[n]
	if n == 0:
		q = 0
	else:
		q = -sys.maxsize
		for i in range(1,n+1): 
			q = max( q, p[i] + memoized_cut_rod_helper(p,n-i,r))
	r[n] = q 
	return q

```

# Constructing path to optimal solution (top-down)
```python
def memoized_cut_rod_sol(p,n):
	r = [-1] * (n+1)
	s = [-1] * (n+1)
	return memoized_cut_rod_helper_sol(p,n,r,s,0)

def memoized_cut_rod_helper_sol(p,n,r,s,counter):
	first_cut = 0
	if r[n] >= 0:
		return r[n]
	if n == 0:
		q = 0
	else:
		q = -sys.maxsize
		for i in range(1,n+1): 
			new = memoized_cut_rod_helper_sol(p,n-i,r,s,counter+1)
			if q < p[i] + new:
				q = p[i] + new
				first_cut = i
	r[n] = q 
	s[n] = first_cut
		
	if(counter == 0):
		return q,s
	else:
		return q

def print_sol(p,n):
	r,s = memoized_cut_rod_sol(p,n)
	print("Revenue : " , r)
	while(n > 0):
		print(s[n] , end=',')
		n = n - s[n]
	print('\n')

```

# Bottom Up Approach 
```python 
def bottom_up_cut_rod(p,n):
	r = [0] * (n+1)
	for j in range(1,n+1):
		q = -sys.maxsize
		for i in range(1,j+1):
			q = max(q,p[i]+r[j-i])
		r[j] = q
	return r[n]
```


# Constructing path to optimal solution (bottom-up)
```python
def bottom_up_cut_rod_sol(p,n):
	r = [0] * (n+1)
	s = [0] * (n+1)
	for j in range(1,n+1):
		q = -1
		for i in range(1,j+1):
			if q < p[i]+r[j-i]:
				q = p[i] + r[j-i]
				s[j] = i
		r[j] = q
	return r[n],s

def print_sol(p,n):
	r,s = bottom_up_cut_rod_sol(p,n)
	while(n > 0):
		print(s[n] , end=',')
		n = n - s[n]
	print('\nMax Revenue is ' , r , '\n')
```
