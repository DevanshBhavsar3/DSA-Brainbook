01-08-2025  17:28

Status: #Revision-03 

Tags: [[Tags/DSA]] [[Stack]]

# Postfix to Prefix Conversion

https://www.naukri.com/code360/problems/postfix-to-prefix_1788455


- Start iterating postfix expression.
- If it is an operand add it to ans.
- Else, get the last 2 operands and put the operator before operands and add it to stack.


```cpp
#include <bits/stdc++.h>

string postfixToPrefix(string &s){
    stack<string> st;
	
    for(int i = 0; i < s.size(); i++) {
        if((s[i] >= 'A' && s[i] <= 'Z') ||
        (s[i] >= 'a' && s[i] <= 'z') ||
        (s[i] >= '0' && s[i] <= '9')) {
            st.push(string(1, s[i]));
        } else {
            string op1 = st.top();
            st.pop();
			
            string op2 = st.top();
            st.pop();
			
            string newOp = s[i] + op2 + op1;
			
            st.push(newOp);
        }
    }
	
    return st.top();
}
```

|      **Time Complexity**      | **Space Complexity** |
| :---------------------------: | :------------------: |
| $O(N) + O(N)$, Adding strings |        $O(N)$        |





# References

[[Prefix, Infix and Postfix Conversions]]