14-09-2025  16:05

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Sliding Window & Two Pointers Problems]]

# Max Consecutive Ones III

https://leetcode.com/problems/max-consecutive-ones-iii/

### Brute Force

- Return the maximum length from all the subarray with at most k zeros.

```cpp
class Solution {
public:
    int longestOnes(vector<int>& nums, int k) {
        int longest = 0;
        
        for(int i = 0; i < nums.size(); i++) {
            int zeroCnt = 0;
            
            for(int j = i; j < nums.size(); j++) {
                if(nums[j] == 0) {
                    zeroCnt++;
                }
                
                if(zeroCnt <= k) {
                    longest = max(longest, j - i + 1);
                } else {
                    break;
                }
            }
        }
        
        return longest;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(1)$        |


### Better

- Create a sliding window with at most k zeros.
- If zeros are > k, move left until 1 zero is removed.

```cpp
class Solution {
public:
    int longestOnes(vector<int>& nums, int k) {
        int longest = 0;
        
        int left = 0;
        int right = 0;
        
        int zeroCnt = 0;
        
        while(right < nums.size()) {
            if(nums[right] == 0) {
                zeroCnt++;
            }
            
            while(zeroCnt > k) {
                if(nums[left] == 0) {
                    zeroCnt--;
                }
                
                left++;
            }
            
            longest = max(longest, right - left + 1);
            right++;
        }
        
        return longest;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |        $O(1)$        |


### Optimal

- Create a sliding window with at most k zeros.
- If zeros are > k, move both left and right.
- Only update the ans, if the zeros are <= k.

> This works because whenever the zeros > k, the minimum length you need to change the ans is, current longest + 1.
> So to optimize the time complexity, you can move the entire window.

```cpp
class Solution {
public:
    int longestOnes(vector<int>& nums, int k) {
        int longest = 0;
        
        int left = 0;
        int right = 0;
        
        int zeroCnt = 0;
        
        while(right < nums.size()) {
            if(nums[right] == 0) {
                zeroCnt++;
            }
            
            if(zeroCnt > k) {
                if(nums[left] == 0) {
                    zeroCnt--;
                }
                
                left++;
            } 
            
            if(zeroCnt <= k) {
                longest = max(longest, right - left + 1);
            }
            
            right++;
        }
        
        return longest;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References