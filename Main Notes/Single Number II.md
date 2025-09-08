25-07-2025  15:49

Status: #Revision-02 

Tags: [[Tags/DSA]] [[Bit Manipulation]]

# Single Number II

https://leetcode.com/problems/single-number-ii/description/

## Brute Force

[[Single Number#Brute Force]]


## Better

- For every bit of int (32) check how many times that bit is set in the nums array.
- If the count is not multiple of 3, that means the single no. has that bit set.
- Set that bit in the ans variable.


```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ans = 0;
		
        for(int i = 0; i < 32; i++) {
            int cnt = 0;
			
            for(int j = 0; j < nums.size(); j++) {
                if(nums[j] & (1 << i)) {
                    cnt++;
                }
            }
			
            if(cnt % 3 == 1) {
                ans = ans | (1 << i);
            }
        }
		
        return ans;
    }
};
```


| **Time Complexity** | **Space Complexity** |
| ------------------- | -------------------- |
| $O(32) * O(n)$      | $O(1)$               |


## More Better

```
2 2 1 2 1 1 4 3 4 4

1 1 1 2 2 2 3 4 4 4
  ^     ^   - ^
```


- Sort the array.
- For every cluster go to the middle element and check if the previous element is same as current one.
- If not return the previous element.


```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end());
		
        for(int i = 1; i < nums.size(); i += 3) {
            if(nums[i] != nums[i - 1]) {
                return nums[i - 1];
            }
        }
		
        return nums[nums.size() - 1];
    }
};
```


| **Time Complexity**      | **Space Complexity** |
| ------------------------ | -------------------- |
| $O(n \log n) * O(n / 3)$ | $O(1)$               |

> This is better than previous solution because to become O(32) as prev one, this solution required nums size to be $2^{32}$ , which is very big.



## Optimal

- Add to one ( nums[i] ^ one ), if it is not in two ( ~two ).
- Add to two ( nums[i] ^ two  ), if it is not in one ( ~one ).

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int one = 0;
        int two = 0;
		
        for(int i = 0; i < nums.size(); i++) {
            one = (nums[i] ^ one) & ~two;
            two = (nums[i] ^ two) & ~one;
        }
		
        return one;
    }
};
```


| **Time Complexity** | **Space Complexity** |
| ------------------- | -------------------- |
| $O(N)$              | $O(1)$               |

# References