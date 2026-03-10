04-03-2026  16:29

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Subset Sum Equal to K

https://www.naukri.com/code360/problems/subset-sum-equal-to-k_1550954

## Memoization

- Generate every possible subsequence of the array by picking or ignoring an element.
- If you pick an element for the subsequence reduce the target by that element.
- Return true if the target becomes 0.
- Memoize the ans at a particular index with target value.

```cpp
#include <bits/stdc++.h>

bool check(int idx, int n, int k, vector<int>& arr, vector<vector<int>>& dp) {
    if(k == 0) {
        return true;
    } else if(k < 0) {
        return false;
    } else if(idx >= n) {
        return false;
    }
	
    if(dp[idx][k] != -1) {
        return dp[idx][k];
    }
	
    return dp[idx][k] = (check(idx + 1, n, k - arr[idx], arr, dp) || check(idx + 1, n, k, arr, dp));
}

bool subsetSumToK(int n, int k, vector<int> &arr) {
    vector<vector<int>> dp(n, vector<int>(k + 1, -1));
	
    return check(0, n, k, arr, dp);
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*K)$       |     $O(N*K + N)$     |


## Tabulation

```cpp
#include <bits/stdc++.h>


bool subsetSumToK(int n, int k, vector<int> &arr) {
    vector<vector<bool>> dp(n, vector<bool>(k + 1, false));
	
	if(arr[0] <= k) {
        dp[0][arr[0]] = true;
    }
	
    for(int i = 0; i < n; i++) {
        dp[i][0] = true;
    }
	
    for(int i = 1; i < n; i++) {
        for(int j = 1; j <= k; j++) {
            dp[i][j] = ((arr[i] <= j) ? dp[i - 1][j - arr[i]] : false) || dp[i - 1][j];
        }
    }
	
    return dp[n - 1][k];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(N * K)$      |      $O(N * K)$      |
### Space Optimization

```cpp
#include <bits/stdc++.h>

bool subsetSumToK(int n, int k, vector<int> &arr) {
    vector<bool> prev(k + 1, false);
    prev[0] = true;
	
	if(arr[0] <= k) {
        prev[arr[0]] = true;
    }
	
    for(int i = 1; i < n; i++) {
        vector<bool> tmp(k + 1, false);
        tmp[0] = 1;
		
        for(int j = 1; j <= k; j++) {
            tmp[j] = ((arr[i] <= j) ? prev[j - arr[i]] : false) || prev[j];
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