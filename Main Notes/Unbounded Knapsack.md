10-03-2026  14:48

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Unbounded Knapsack

https://www.naukri.com/code360/problems/unbounded-knapsack_1215029

## Memoization

- Use pick & not pick algorithm.
- If you pick an item, you can stay at the same index and choose that item again.
- At index 0, you can select `knapsack size / weights[0]` items and can return total profit.
- Memoize the knapsack size at every index.

```cpp
#include<bits/stdc++.h>

int f(int idx, int w, vector<int>& profit, vector<int>& weight, vector<vector<int>>& dp) {
    if(idx == 0) {
        return profit[0] * (w / weight[0]);
    }
	
    if(dp[idx][w] != -1) {
        return dp[idx][w];
    }
	
    int notPick = f(idx - 1, w, profit, weight, dp);
    int pick = INT_MIN;
    
    if(weight[idx] <= w) {
        pick = f(idx, w - weight[idx], profit, weight, dp) + profit[idx];
    }
	
    return dp[idx][w] = max(pick, notPick);
}

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight){
    vector<vector<int>> dp(n, vector<int>(w + 1, -1));
	
    return f(n - 1, w, profit, weight, dp);
}
```

| **Time Complexity** |     **Space Complexity**      |
| :-----------------: | :---------------------------: |
|      $O(N*W)$       | $O(N*W + \text{Stack Space})$ |


## Tabulation

```cpp
#include<bits/stdc++.h>

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight){
    vector<vector<int>> dp(n, vector<int>(w + 1));
	
    for(int i = 0; i <= w; i++) {
        dp[0][i] = profit[0] * (i / weight[0]);
    }
	
    for(int i = 1; i < n; i++) {
        for(int j = 0; j <= w; j++) {
            int notPick = dp[i - 1][j];
            int pick = INT_MIN;
            
            if(weight[i] <= j) {
                pick = dp[i][j - weight[i]] + profit[i];
            }
			
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
#include<bits/stdc++.h>

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight){
    vector<int> prev(w + 1);
	
    for(int i = 0; i <= w; i++) {
        prev[i] = profit[0] * (i / weight[0]);
    }
	
    for(int i = 1; i < n; i++) {
        for(int j = 0; j <= w; j++) {
            int notPick = prev[j];
            int pick = INT_MIN;
            
            if(weight[i] <= j) {
                pick = prev[j - weight[i]] + profit[i];
            }
			
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