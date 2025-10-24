24-09-2025  15:20

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Jump Game II

https://leetcode.com/problems/jump-game-ii/

### Brute Force

- For each index, try out all the possible jumps to reach to N - 1.
- Return min of all jumps.

```cpp
class Solution {
public:
    int jumpAll(vector<int>& nums, int idx, int jumps) {
        if(idx >= nums.size() - 1) {
            return jumps;
        }
        
        int mini = INT_MAX;
        
        for(int i = 1; i <= nums[idx]; i++) {
            mini = min(mini, jumpAll(nums, idx + i, jumps + 1));
        }
        
        return mini;
    }
    
    int jump(vector<int>& nums) {
        return jumpAll(nums, 0, 0);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^N)$       |        $O(N)$        |


### Optimal

- At each window, find out the maximum index you can reach.
- Move right to left + 1, and left to the maximum index.
- Increase jump count at each step, until right reaches N - 1.

```cpp
class Solution {
public:
    int jump(vector<int>& nums) {
        int left = 0;
        int right = 0;
        
        int jumps = 0;
        
        while(right < nums.size() - 1) {
            int farthest = 0;
            
            for(int i = left; i <= right; i++) {
                farthest = max(farthest, i + nums[i]);
            }
            
            left = right + 1;
            right = farthest;
            
            jumps++;
        }
        
        return jumps;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References