10-11-2025  15:40

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Remove Outermost Parentheses

https://leetcode.com/problems/remove-outermost-parentheses/

- Create opened parentheses counter.
- When opening parentheses occur, first check if it the outermost one or not. If not then add to ans.
- After closing parentheses, check if it was the outermost one or not, if not add to ans.

```cpp
class Solution {
public:
    string removeOuterParentheses(string s) {
        string ans;
        int opened = 0;
		
        for(int i = 0; i < s.size(); i++) {
            if(s[i] == '(') {
                if(opened > 0) {
                    ans += s[i];
                }
				
                opened++;
            } else {
                opened--;
                
                if(opened > 0) {
                    ans += s[i];
                }
            }            
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References