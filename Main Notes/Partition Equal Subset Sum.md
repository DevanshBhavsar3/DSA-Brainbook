05-03-2026  15:26

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Partition Equal Subset Sum

https://leetcode.com/problems/partition-equal-subset-sum/

## Memoization

- 2 equal sum subsets are only possible if the total of the elements is even.
- So we can find only 1 subset which have sum equal to total / 2.
- Then the problem becomes same as subset sum equals to k.

```cpp
class Solution {
public:
    bool partition(int idx, int target, vector<int>& nums, vector<vector<int>>& dp) {
        if(target == 0) {
            return true;
        } else if(target < 0) {
            return false;
        } else if(idx == 0) {
            return nums[0] == target;
        }
		
        if(dp[idx][target] != -1) {
            return dp[idx][target];
        }
		
        return dp[idx][target] = partition(idx - 1, target - nums[idx], nums, dp) || partition(idx - 1, target, nums, dp);
    }    
	
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
		
        int total = 0;
        for(int i = 0; i < nums.size(); i++) {
            total += nums[i];
        }
		
        if(total & 1) {
            return false;
        }
	
		vector<vector<int>> dp(n, vector<int>((total / 2) + 1, -1));
		
        return partition(nums.size() - 1, total / 2, nums, dp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(N * K)$      |    $O(N * K + N)$    |
$K = \text{TOTAL} / 2$


## Tabulation

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
		
        int total = 0;
        for(int i = 0; i < nums.size(); i++) {
            total += nums[i];
        }
		
        if(total & 1) {
            return false;
        }
		
        int k = total / 2;
		
        vector<vector<bool>> dp(n, vector<bool>(k + 1, false));
		
        for(int i = 0; i < n; i++) {
            dp[i][0] = true;
        }
		
        if(nums[0] <= k) {
            dp[0][nums[0]] = true;
        }
		
        for(int i = 1; i < n; i++) {
            for(int j = 1; j <= k; j++) {
                dp[i][j] = ((nums[i] <= j) ? dp[i - 1][j - nums[i]] : false) || dp[i - 1][j];
            }
        }
		
        return dp[n - 1][k];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*K)$       |       $O(N*K)$       |
$K = \text{TOTAL} / 2$
### Space Optimization

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
		
        int total = 0;
        for(int i = 0; i < nums.size(); i++) {
            total += nums[i];
        }
		
        if(total & 1) {
            return false;
        }
		
        int k = total / 2;
		
        vector<bool> prev(k + 1, false);
        prev[0] = true;
		
        if(nums[0] <= k) {
            prev[nums[0]] = true;
        }
		
        for(int i = 1; i < n; i++) {
            vector<bool> tmp(k + 1, false);
			
            for(int j = 1; j <= k; j++) {
                tmp[j] = ((nums[i] <= j) ? prev[j - nums[i]] : false) || prev[j];
            }
			
            prev = tmp;
        }
		
        return prev[k];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*K)$       |        $O(K)$        |
$K = \text{TOTAL} / 2$





# References
[[Subset Sum Equal to K]]