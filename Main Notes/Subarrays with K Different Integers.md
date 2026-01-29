19-09-2025  15:54

Status: #Revision-03

Tags: [[Tags/DSA|DSA]] [[Sliding Window & Two Pointers Problems]]

# Subarrays with K Different Integers

https://leetcode.com/problems/subarrays-with-k-different-integers/

### Brute Force

- Iterate over all the subarrays while hashing each number with its frequencies.
- If map size == k, increase the ans.
- else If map size is > k, break the loop.

```cpp
class Solution {
public:
    int subarraysWithKDistinct(vector<int>& nums, int k) {
        map<int, int> mp;
        int ans = 0;
        
        for(int i = 0; i < nums.size(); i++) {
            for(int j = i; j < nums.size(); j++) {
                mp[nums[j]]++;
                
                if(mp.size() == k) {
                    ans++;
                } else if(mp.size() > k) {
                    break;
                }
            }
            
            mp.clear();
        }
        
        return ans;
    }
};
```

|                                   **Time Complexity**                                    | **Space Complexity** |
| :--------------------------------------------------------------------------------------: | :------------------: |
| $O(N^2)$ +<br>$O(\log N)$ (Map), <br><br>$O(N)$ (Unordered Map)<br>$O(N^2)$ (Worst Case) |        $O(N)$        |


### Optimal

- Find total subarrays with distinct numbers<= k.
- Subtract the total with total subarrays with distinct numbers <= k - 1.

- When finding total subarrays with distinct numbers <= k,
	- If the window has more than k distinct numbers, shrink the window until it is <= k.
	- The total count is increased by left - right + 1 ( window size ) in valid window.

```cpp
class Solution {
public:
    int subarraysWithLessEqualKDistinct(vector<int>& nums, int k) {
        if(k <= 0) return 0;
        
        map<int, int> mp;
        
        int left = 0;
        int right = 0;   
        
        int ans = 0;
        
        while(right < nums.size()) {
            mp[nums[right]]++;
            
            while(mp.size() > k) {
                mp[nums[left]]--;
                
                if(mp[nums[left]] == 0) {
                    mp.erase(nums[left]);
                }
                
                left++;
            }
            
            ans += right - left + 1;
            
            right++;
        }
        
        return ans;
    } 
    
    int subarraysWithKDistinct(vector<int>& nums, int k) {
        return subarraysWithLessEqualKDistinct(nums, k) - subarraysWithLessEqualKDistinct(nums, k - 1);
    }
};
```

|                                       **Time Complexity**                                       | **Space Complexity** |
| :---------------------------------------------------------------------------------------------: | :------------------: |
| $O(4N)$ +<br>$O(2 * \log N)$ (Map), <br><br>$O(1)$ (Unordered Map)<br>$O(2 * N^2)$ (Worst Case) |       $O(2N)$        |





# References