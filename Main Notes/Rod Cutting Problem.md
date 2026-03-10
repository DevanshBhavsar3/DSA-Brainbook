10-03-2026  16:07

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Rod Cutting Problem

https://www.naukri.com/code360/problems/rod-cutting-problem_800284

## Memoization

- The index in the recursion will represent the maximum profit you can have with the rod length of n and maximum cut being index + 1.
- Use the pick & not pick algorithm.
- If you pick an index, you can stay at the same index and choose that index again.
- At index 0, the maximum profit you can achieve with max cut being 1 is `Rod Length * price[0]`.
- Memoize the rod size at every index.

```cpp
int cut(int idx, int n, vector<int>& price, vector<vector<int>>& dp) {
	if(idx == 0) {
		return price[idx] * n;
	}
	
	if(dp[idx][n] != -1) {
		return dp[idx][n];
	}
	
	int notPick = cut(idx - 1, n, price, dp);
	int pick = INT_MIN;
	
	if(idx + 1 <= n) {
		pick = cut(idx, n - idx - 1, price, dp) + price[idx];
	}
	
	return dp[idx][n] = max(pick, notPick);
}

int cutRod(vector<int> &price, int n)
{
	vector<vector<int>> dp(n, vector<int>(n + 1, -1));
	
	return cut(n - 1, n, price, dp);
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*N)$       |     $O(N*N +N)$      |


## Tabulation

```cpp
int cutRod(vector<int> &price, int n)
{
	vector<vector<int>> dp(n, vector<int>(n + 1, -1));
	
	for(int i = 0; i <= n; i++) {
		dp[0][i] = i * price[0];
	}
	
	
	for(int i = 1; i < n; i++) {
		for(int j = 0; j <= n; j++) {
			int notPick = dp[i - 1][j];
			int pick = INT_MIN;
			
			if(i + 1 <= j) {
				pick = dp[i][j - i - 1] + price[i];
			}
			
			dp[i][j] = max(pick, notPick);
		}
	}
	
	return dp[n - 1][n];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*N)$       |       $O(N*N)$       |
### Space Optimization

```cpp
int cutRod(vector<int> &price, int n)
{
	vector<int> prev(n + 1, -1);
	
	for(int i = 0; i <= n; i++) {
		prev[i] = i * price[0];
	}
	
	
	for(int i = 1; i < n; i++) {
		for(int j = 0; j <= n; j++) {
			int notPick = prev[j];
			int pick = INT_MIN;
			
			if(i + 1 <= j) {
				pick = prev[j - i - 1] + price[i];
			}
			
			prev[j] = max(pick, notPick);
		}
	}
	
	return prev[n];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*N)$       |        $O(N)$        |





# References