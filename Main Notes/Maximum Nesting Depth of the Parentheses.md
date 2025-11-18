14-11-2025  15:16

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Maximum Nesting Depth of the Parentheses

https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/

- Find maximum opened parentheses at any time.

```cpp
class Solution {
public:
    int maxDepth(string s) {
        int maxi = 0;
        int opened = 0;
		
        for(int i = 0; i < s.size(); i++) {
            if(s[i] == '(') {
                opened++;
            } else if(s[i] == ')') {
                opened--;
            }
			
            maxi = max(maxi, opened);
        }
		
        return maxi;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References