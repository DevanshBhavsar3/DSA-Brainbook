30-07-2025  15:28

Status: #Revision 

Tags: [[Tags/DSA]] [[Stack]]

# Valid Parentheses

https://leetcode.com/problems/valid-parentheses/description/


- Push opening parentheses to stack.
- When a closing parentheses occur, check if the last opening parentheses is the same.
- Else return false.


```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
		
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(' || s[i] == '{' || s[i] == '[') {
                st.push(s[i]);
            } else {
                if (st.empty()) {
                    return false;
                }
                    
                char ch = st.top();
                st.pop();
				
                if ((s[i] == ')' && ch == '(') || (s[i] == '}' && ch == '{') ||
                    (s[i] == ']' && ch == '[')) {
				
                } else {
                    return false;
                }
            }
        }
		
        return st.empty();
    }
};
```


| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References