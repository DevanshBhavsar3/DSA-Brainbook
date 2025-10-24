24-09-2025  14:57

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Jump Game

https://leetcode.com/problems/jump-game/

- Count where you can maximum go standing at every index.
- If you can go till nums.size() - 1, return true;

```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int maxIndex = 0;
        
        for(int i = 0; i < nums.size() - 1; i++) {
	        // No jump combination come to this i
            if(i > maxIndex) {
                return false;
            }
            
            maxIndex = max(maxIndex, i + nums[i]);
        }
        
        return maxIndex >= nums.size() - 1;
    }
}; 
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References