06-03-2026  15:52

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Count Subsets with Sum K

https://www.naukri.com/code360/problems/count-subsets-with-sum-k_3952532

## Memoization

- Use pick & not pick algorithms to find all the possible subsets with sum K.
- If the index becomes < 0 and the target is 0, return 1.
- Memoize the target at every index.

```cpp
int find(int idx, int k, vector<int>& arr, vector<vector<int>>& dp) {
	if(idx < 0) {
		return k == 0;
	}
	
	if(dp[idx][k] != -1) {
		return dp[idx][k];
	}
	
	int notPick = find(idx - 1, k, arr, dp);
	int pick = 0;
	
	if(arr[idx] <= k) {
		pick = find(idx - 1, k - arr[idx], arr, dp);
	}
	
	return dp[idx][k] = (pick + notPick) % ((int) 1e9 + 7);
}

int findWays(vector<int>& arr, int k)
{
	int n = arr.size();
	vector<vector<int>> dp(n, vector<int>(k + 1, -1));
	
	return find(n - 1, k, arr, dp);
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(N * K)$      |    $O(N * K + N)$    |


## Tabulation

```cpp
int findWays(vector<int>& arr, int k) {
	int n = arr.size();
	vector<vector<int>> dp(n, vector<int>(k + 1, -1));
	
	for(int i = 0; i < n; i++) {
		for(int j = 0; j <= k; j++) {
			// If not pick the first index, target should be 0
			int notPick = (i != 0) ? dp[i - 1][j] : j == 0;
			int pick = 0;
			
			// if pick the first index, target should become 0 (j - arr[i] == 0)
			if(arr[i] <= j) {
				pick = (i != 0) ? dp[i - 1][j - arr[i]]: j == arr[i];
			}
			
			dp[i][j] = (pick + notPick) % ((int) 1e9 + 7);
		}
	}
	
	return dp[n - 1][k];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*K)$       |       $O(N*K)$       |
### Space Optimization

```cpp
int findWays(vector<int>& arr, int k) {
	int n = arr.size();
	vector<int> prev(k + 1, 0);
	
	prev[0] = 1;
	
	for(int i = 0; i < n; i++) {
		vector<int> tmp(k + 1, 0);
		
		for(int j = 0; j <= k; j++) {
			int notPick = prev[j];
			int pick = 0;
			
			if(arr[i] <= j) {
				pick = prev[j - arr[i]];
			}
			
			tmp[j] = (pick + notPick) % ((int) 1e9 + 7);
		}
		
		prev = tmp;
	}
	
	return prev[k];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(N * K)$      |        $O(K)$        |





# References