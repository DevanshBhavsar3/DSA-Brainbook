17-09-2025  14:58

Status: #Revision-03

Tags: [[Tags/DSA|DSA]] [[Sliding Window & Two Pointers Problems]]

# Binary Subarrays With Sum

https://leetcode.com/problems/binary-subarrays-with-sum/

### Brute Force

- Count total subarrays with total sum = goal.

```cpp
class Solution {
public:
    int numSubarraysWithSum(vector<int>& nums, int goal) {
        int ans = 0;
        
        for(int i = 0; i < nums.size(); i++) {
            int total = 0;
            
            for(int j = i; j < nums.size(); j++) {
                total += nums[j];
                
                if(total > goal) {
                    break;
                }
                
                if(total == goal) {
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


### Better

```cpp
class Solution {
public:
    int numSubarraysWithSum(vector<int>& nums, int goal) {
        map<int, int> mp;
        int prefix = 0;
        int total = 0;
		
        mp[0] = 1;
		
        for(int i = 0; i < nums.size(); i++) {
            prefix += nums[i];
			
            if(mp.find(prefix - goal) != mp.end()) {
                total += mp[prefix - goal];
            }
			
            mp[prefix]++;
        }
		
        return total;
    }
};
```


### Optimal

```
1 0 0 1 1 0, goal = 2
L
R

ans = 1

--

1 0 0 1 1 0, goal = 2
L
  R
  
ans = 1 + 2

-- 
  
1 0 0 1 1 0, goal = 2
L
    R

ans = 1 + 2 + 3 + ...
```

- Find total subarrays <= goal.
- Subtract the total with total subarrays <= goal - 1.

```cpp
class Solution {
public:
	// O(2N)
    int numSubarraysWithLessEqualSum(vector<int>& nums, int goal) {
        if(goal < 0) {
            return 0;
        }
        
        int ans = 0;
        
        int left = 0;
        int right = 0;
        
        int cnt = 0;
        
        while(right < nums.size()) {
            cnt += nums[right];
            
            while(cnt > goal) {
                cnt -= nums[left];
                left++;
            }
            
            
            // Length of the window are new subarrays with sum <= goal
            ans += right - left + 1;
            right++;
        }
        
        return ans;
    }
    
    int numSubarraysWithSum(vector<int>& nums, int goal) {
        return numSubarraysWithLessEqualSum(nums, goal) - numSubarraysWithLessEqualSum(nums, goal - 1);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(4N)$       |        $O(1)$        |





# References