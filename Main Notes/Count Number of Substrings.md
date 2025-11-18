18-11-2025  15:04

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Count Number of Substrings

https://www.geeksforgeeks.org/problems/count-number-of-substrings4528/1

- Count no. of substrings with <= k and <= k - 1 distinct characters.
- Return the subtraction of that.

```cpp
class Solution {
public:
    int cntLessOrEqual(string& s, int k) {
        if(k <= 0) {
            return 0;
        }
        
        int total = 0;
        unordered_map<char, int> mp;
        
        int left = 0;
        int right = 0;
        
        while(right < s.size()) {
            mp[s[right]]++;
            
            while(mp.size() > k) {
                mp[s[left]]--;
                
                if(mp[s[left]] == 0) {
                    mp.erase(s[left]);
                }
                
                left++;
            }
            
            total += right - left + 1;
            right++;
        }
        
        return total;
    }
	
    int countSubstr(string& s, int k) {
        return cntLessOrEqual(s, k) - cntLessOrEqual(s, k - 1);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(4N)$       |        $O(1)$        |





# References