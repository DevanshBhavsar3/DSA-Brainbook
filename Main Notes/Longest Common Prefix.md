11-11-2025  14:43

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Longest Common Prefix

https://leetcode.com/problems/longest-common-prefix/

- Sort all the strings, so it will be sorted in lexicographical order.
- Now just compare the first and the last string to determine the prefix.

```cpp
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        sort(strs.begin(), strs.end());
		
        string ans = "";
		
        string first = strs[0];
        string last = strs.back();
		
        for(int i = 0; i < first.size(); i++) {
            if(first[i] != last[i]) {
                break;
            }
			
            ans += first[i];
        }
		
        return ans;
    }
};
```

> All the strings between first and last will have common prefix after sorting.

| **Time Complexity**  |           **Space Complexity**           |
| :------------------: | :--------------------------------------: |
| $O(N \log N) + O(M)$ | $O(M)$, M = minimum length of the string |





# References