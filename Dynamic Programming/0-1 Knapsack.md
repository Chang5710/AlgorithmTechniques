``` Written By : DIAO  6/11/20 ```
# 0-1 Knapsack  
```
Recursive Formula : 
                0  if i == 0 or j == 0
napsack(i,j) =  napsack(i-1 , j) , elif w[i] > j
                max(v[i] + napsack(i-1,j-w[i]))  , else 


```

# Top Down  Approach 
```python
def knapsack(w,v,n,c):
	dp = [[-1]*(c+1) for _ in range(n+1)]

	res = helper(w,v,n,c,dp)
	for row in dp:
		print(row)
	print("\nMax Revenue {}".format(res))


def helper(w,v,n,c,dp):
	if dp[n][c] > -1:
		return dp[n][c]
	
	if n == 0 or c == 0:
		dp[n][c] = 0
		return 0

	if w[n] > c:
		dp[n][c] = dp[n-1][c]
	else:
		dp[n][c] = max( v[n] + helper(w,v,n-1,c-w[n],dp) , helper(w,v,n-1,c,dp))

	return dp[n][c] 


if __name__ == "__main__":
	w = [0,2,3,5]
	v = [0,3,4,6]
	napsack(w,v,3,8)
```

# Bottom Up Approach 
```python 
def knapsack(w,v,n,c):
	dp = [[0]*(c+1) for _ in range(n+1)]

	for i in range(1,n+1):
		for j in range(1,c+1):
			if w[i] > j:
				dp[i][j] = dp[i-1][j]
			else:
				dp[i][j] = max(v[i] + dp[i-1][j-w[i]] , dp[i-1][j])

	# Print dp table content 
	for row in dp:
		print(row)
	# Print Solution 
	print("\nMax Value is " , dp[n][c])
	for item in range(n, 0 , -1):
		if(dp[item][c] > dp[item-1][c]):
			print("Take item :" , item)
			c -= w[item]


if __name__ == "__main__":
	w = [0,2,3,5]
	v = [0,3,4,6]
	napsack(w,v,3,8)

```