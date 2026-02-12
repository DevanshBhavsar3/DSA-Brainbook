11-02-2026  17:05

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Maximum Sum Of Non Adjacent Elements

https://leetcode.com/problems/house-robber/

## Memoization

- Use a pick & not pick algorithm to generate all the subsequences.
- Whenever you pick an index, you can not pick subsequent index (index - 2).
- At index 0, you can only pick it.
- Return the maximum amount at the end.

```cpp
class Solution {
public:
    int breakInHouse(int idx, vector<int>& nums, vector<int>& dp) {
        if(idx < 0) {
            return 0;
        } else if(idx == 0) {
            return nums[0];
        }
		
        if(dp[idx] != -1) {
            return dp[idx];
        }
		
        return dp[idx] = max(breakInHouse(idx - 2, nums, dp) + nums[idx], breakInHouse(idx - 1, nums, dp));
    }
	
    int rob(vector<int>& nums) {
        vector<int> dp(nums.size(), -1);
		
        return breakInHouse(nums.size() - 1, nums, dp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |       $O(2N)$        |


## Tabulation

- Create a dp array with all the base case.
- Only add the previous amount if it is a valid index.
- Iterate till n, and calculate the maximum amount.
- Return the (n - 1)th result.

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
		
        vector<int> dp(n);
        dp[0] = nums[0];
		
        for(int i = 1; i < n; i++) {
            int maxi = max(dp[i - 1], nums[i] + ((i > 1) ? dp[i - 2]: 0));
            dp[i] = maxi;
        }
		
        return dp[n - 1];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |
### Space Optimization

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
		
        int prev = nums[0];
        int prev2 = 0;
		
        for(int i = 1; i < n; i++) {
            int tmp = prev;
            prev = max(prev, nums[i] + prev2);
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