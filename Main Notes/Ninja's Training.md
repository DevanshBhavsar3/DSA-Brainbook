13-02-2026  16:55

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Ninja's Training

https://www.naukri.com/code360/problems/ninja-s-training_3621003

## Memoization

- For each day perform a task that was not previously performed & go for the next day while passing the performed task index.
- Find the maximum points from all the task performed.
- Use a dp matrix of size $N * 4$ to memoize the result for a particular day and a previous task.

```cpp
#include <bits/stdc++.h>

int train(int day, int prev, vector<vector<int>>& points, vector<vector<int>>& dp) {
    if(day < 0) {
        return 0;
    }
	
    if(dp[day][prev] != -1) {
        return dp[day][prev];
    }
	
    int maxi = INT_MIN;
	
    for(int i = 0; i < 3; i++) {
        if(i == prev) {
            continue;
        }
		
        maxi = max(maxi, train(day - 1, i, points, dp) + points[day][i]);
    }
	
    return dp[day][prev] = maxi;
}

int ninjaTraining(int n, vector<vector<int>> &points)
{
    vector<vector<int>> dp(n, vector<int>(4, -1));
	
    return train(n - 1, 3, points, dp);
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(3*(N*4))$     |     $O(N*4 + N)$     |


## Tabulation

- Create a dp array of size $N * 4$.
- For each day and each presumably next task, perform all the valid task.
- Update the `dp[day][next]` with the maximum points for that day and that task.

```cpp
#include <bits/stdc++.h>

int ninjaTraining(int n, vector<vector<int>> &points)
{
    vector<vector<int>> dp(n, vector<int>(4, -1));
	
    for(int day = 0; day < n; day++) {
        for(int next = 0; next < 4; next++) {
            for(int task = 0 ; task < 3; task++) {
                if(task == next) {
                    continue;
                }
                
                int p = ((day > 0) ? dp[day - 1][task] : 0) + points[day][task];
                dp[day][next] = max(dp[day][next], p);
            }
        }
    }
	
    return dp[n - 1][3];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(N*4*3)$      |       $O(N*4)$       |
### Space Optimization

```cpp
#include <bits/stdc++.h>

int ninjaTraining(int n, vector<vector<int>> &points)
{
    vector<int> prev(4, 0);
	
    for(int day = 0; day < n; day++) {
        vector<int> tmp(4);
		
        for(int next = 0; next < 4; next++) {
            for(int task = 0 ; task < 3; task++) {
                if(task == next) {
                    continue;
                }
                
                int p = prev[task] + points[day][task];
                tmp[next] = max(tmp[next], p);
            }
        }
		
        prev = tmp;
    }
	
    return prev[3];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|   $O*(N * 4 * 3)$   |        $O(1)$        |





# References