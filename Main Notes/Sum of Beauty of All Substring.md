18-11-2025  16:51

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Sum of Beauty of All Substring

https://leetcode.com/problems/sum-of-beauty-of-all-substrings/

- For all the substrings, find the max and min frequency of chars.
- Add the subtraction to the total.

```cpp
class Solution {
public:
    int beautySum(string s) {
        int sum = 0;
		
        for(int i = 0; i < s.size(); i++) {
            unordered_map<char, int> mp;
			
            for(int j = i; j < s.size(); j++) {
                mp[s[j]]++;
				
                int maxi = INT_MIN;
                int mini = INT_MAX;
				
                for(auto it: mp) {
                    maxi = max(maxi, it.second);
                    mini = min(mini, it.second);
                }
				
                sum += maxi - mini;
            }
        }
		
        return sum;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(1)$        |





# References