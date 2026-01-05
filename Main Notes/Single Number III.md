25-07-2025  16:49

Status: #Revision-03 

Tags: [[Tags/DSA]] [[Bit Manipulation]]

# Single Number III

https://leetcode.com/problems/single-number-iii/description/

## Brute Force

[[Single Number#Brute Force]]


## Optimal

- Do xor of all the elements.
- Find the different bit ( any set bits from the final xor ).
- Categorize elements based on that bit.
- The final value will be the 2 single values.


```cpp
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        long xr = 0;
		
        for (int i = 0; i < nums.size(); i++) {
            xr ^= nums[i];
        }
		
		// The right most bit
        xr = (xr & (long) xr - 1) ^ xr;
		
        int bucket1 = 0;
        int bucket2 = 0;
		
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] & xr) {
                bucket1 ^= nums[i];
            } else {
                bucket2 ^= nums[i];
            }
        }
		
        return {bucket1, bucket2};
    }
};
```


| **Time Complexity** | **Space Complexity** |
| ------------------- | -------------------- |
| $O(2N)$             | $O(1)$               |


# References