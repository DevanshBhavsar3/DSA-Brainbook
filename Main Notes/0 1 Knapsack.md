08-03-2026  14:33

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# 0 1 Knapsack

https://www.naukri.com/code360/problems/0-1-knapsack_1072980

## Memoization

- The index represents maximum value that can be achieved with knapsack of size w.
- At index 0, you can pick the item and return its value, if the knapsack is big enough.
- Use pick & not pick algorithm, to steal items.
- Return the maximum value from pick or not pick.

```cpp
int steal(int idx, vector<int>& values, vector<int>& weights, int n, int w, vector<vector<int>>& dp) {
	if(idx == 0) {
		if(weights[idx] <= w) {
			return values[idx];
		}
		
		return 0;
	}
	
	if(dp[idx][w] != -1) {
		return dp[idx][w];
	}
	
	int pick = 0;
	if(weights[idx] <= w) {
		pick = steal(idx - 1, values, weights, n, w - weights[idx], dp) + values[idx];
	}
	
	int notPick = steal(idx - 1, values, weights, n, w, dp);
	
	return dp[idx][w] = max(pick, notPick);
}

int maxProfit(vector<int> &values, vector<int> &weights, int n, int w)
{
	vector<vector<int>> dp(n, vector<int>(w + 1, -1));
	
	return steal(n - 1, values, weights, n, w, dp);
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(N * W)$      |    $O(N * W + N)$    |


## Tabulation

```cpp
int maxProfit(vector<int> &values, vector<int> &weights, int n, int w)
{
	vector<vector<int>> dp(n, vector<int>(w + 1, 0));
	
	for(int i = weights[0]; i <= w; i++) {
		dp[0][i] = values[0];
	}
	
	for(int i = 1; i < n; i++) {
		for(int j = 0; j <= w; j++) {
			int pick = 0;
			if(weights[i] <= j) {
				pick = dp[i - 1][j - weights[i]] + values[i];
			}
			
			int notPick = dp[i - 1][j];
			
			dp[i][j] = max(pick, notPick);
		}
	}
	
	return dp[n - 1][w];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*W)$       |       $O(N*W)$       |
### Space Optimization

```cpp
int maxProfit(vector<int> &values, vector<int> &weights, int n, int w)
{
	vector<int> prev(w + 1, 0);
	
	for(int i = weights[0]; i <= w; i++) {
		prev[i] = values[0];
	}
	
	for(int i = 1; i < n; i++) {
		// Start from the maximum weight and store the ans directly in the prev
		for(int j = w; j >= 0; j--) {
			int pick = 0;
			if(weights[i] <= j) {
				pick = prev[j - weights[i]] + values[i];
			}
			
			int notPick = prev[j];
			
			prev[j] = max(pick, notPick);
		}
	}
	
	return prev[w];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*W)$       |        $O(W)$        |





# References