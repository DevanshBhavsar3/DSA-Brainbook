17-09-2025  16:05

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Sliding Window & Two Pointers Problems]]

# Count Number of Nice Subarrays

https://leetcode.com/problems/count-number-of-nice-subarrays/

### Brute Force

- Count total subarrays with total odd numbers == k.

```cpp
class Solution {
public:
    int numberOfSubarrays(vector<int>& nums, int k) {
        int ans = 0;
        
        for(int i = 0; i < nums.size(); i++) {
            int oddCnt = 0;
            
            for(int j = i; j < nums.size(); j++) {
                oddCnt += nums[j] & 1;
                
                if(oddCnt > k) {
                    break;
                }
                
                if(oddCnt == k) {
                    ans++;
                }
            }
        }
        
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(1)$        |


### Optimal

- Imagine odd number as 1, and even numbers as 0.
- Now, it is the same problem as [[Binary Subarrays With Sum]].

```cpp
class Solution {
public:
    int numberOfSubarraysLessEqualSum(vector<int>& nums, int goal) {
        int ans = 0;
        
        int left = 0;
        int right = 0;
        
        int sum = 0;
        
        while(right < nums.size()) {
            sum += nums[right] & 1; // Change
            
            while(sum > goal) {
                sum -= nums[left] & 1; // Change
                left++;
            }
            
            ans += right - left + 1;
            
            right++;
        }
        
        return ans;
    }
    
    int numberOfSubarrays(vector<int>& nums, int k) {
        return numberOfSubarraysLessEqualSum(nums, k) - numberOfSubarraysLessEqualSum(nums, k - 1);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(4N)$       |        $O(1)$        |





# References

[[Binary Subarrays With Sum]]