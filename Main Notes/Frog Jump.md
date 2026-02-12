09-02-2026  16:40

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Frog Jump

https://www.naukri.com/code360/problems/frog-jump_3621012

## Memoization

- For every index, 
	- Find the cost to reach 0 from index + 1 and index + 2.
	- Add the cost to reach that index from current index and find minimum of that.
- Maintain a dp array of size n + 1, that will store the cost to reach 0 for particular index.

```cpp
#include <bits/stdc++.h> 

int jump(int n, vector<int>& heights, vector<int>& dp) {
    if(n == 0) {
        return 0;
    }
	
    if(dp[n] != -1) {
        return dp[n];
    }
	
    int left = jump(n - 1, heights, dp) + abs(heights[n] - heights[n - 1]);
    int right = INT_MAX;
	
    if(n > 1) {
        right = jump(n - 2, heights, dp) + abs(heights[n] - heights[n - 2]);
    }
	
    return dp[n] = min(left, right);
}

int frogJump(int n, vector<int> &heights)
{
    vector<int> dp(n + 1, -1);
    
    return jump(heights.size() - 1, heights, dp);
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |       $O(2N)$        |


## Tabulation

- Store base cases in dp array.
- Iterate till n, and calculate the minimum cost.
- Return the (n - 1)th result.

```cpp
#include <bits/stdc++.h> 

int frogJump(int n, vector<int> &heights)
{
    vector<int> dp(n);
	
    dp[0] = 0;
    dp[1] = abs(heights[1] - heights[0]);
	
    for(int i = 2; i < n; i++) {
        int left = dp[i - 1] + abs(heights[i] - heights[i - 1]);
        int right = dp[i - 2] + abs(heights[i] - heights[i - 2]);
		
        dp[i] = min(left, right);
    }
	
    return dp[n - 1];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |
### Space Optimization

```cpp
#include <bits/stdc++.h> 

int frogJump(int n, vector<int> &heights)
{
    int prev2 = 0;
    int prev = abs(heights[1] - heights[0]);
	
    for(int i = 2; i < n; i++) {
        int left = prev + abs(heights[i] - heights[i - 1]);
        int right = prev2 + abs(heights[i] - heights[i - 2]);
		
        prev2 = prev;
        prev = min(left, right);
    }
	
    return prev;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References