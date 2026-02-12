09-02-2026  16:03

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Climbing Stairs

https://leetcode.com/problems/climbing-stairs/

## Memoization

- Start from N, walk down 1 or 2 steps.
- If you reach 0th step or 1st step return 1, for counting total ways.
- Use dp array to memoize.

```cpp
class Solution {
public:
    int climb(int n, vector<int>& dp) {
        if(n <= 1) {
            return 1;
        }
		
        if(dp[n] != -1) {
            return dp[n];
        }
		
        return dp[n] = climb(n - 1, dp) + climb(n - 2, dp);
    }
	
    int climbStairs(int n) {
        vector<int> dp(n + 1, -1);
		
        return climb(n, dp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |       $O(2N)$        |


## Tabulation

- Instead of recursion use tabulation to count ways to reach down.
- Store results in dp array.

```cpp
class Solution {
public:
    int climbStairs(int n) {
        vector<int> dp(n + 1, -1);
		
        dp[0] = 1;
        dp[1] = 1;
		
        for(int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
		
        return dp[n];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |
### Space Optimization

- We only need the result of previous 2 calculations.
- Store 2 variables instead of an array.

```cpp
class Solution {
public:
    int climbStairs(int n) {
        int prev = 1;
        int prev2 = 1;
		
        for(int i = 2; i <= n; i++) {
            int tmp = prev;
			
            prev = prev + prev2;
            prev2 = tmp;
        }
		
        return prev;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References