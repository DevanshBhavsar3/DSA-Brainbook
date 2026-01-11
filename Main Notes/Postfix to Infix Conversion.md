01-08-2025  17:05

Status: #Revision-03

Tags: [[Tags/DSA]] [[Stack]]

# Postfix to Infix Conversion

https://www.geeksforgeeks.org/problems/postfix-to-infix-conversion/1


- Iterate over all the char in postfix expression.
- If it is an operand add it to stack.
- Else, get the last 2 operands and put the operator in between and cover them in brackets.


```cpp
// User function Template for C++

class Solution {
  public:
    string postToInfix(string exp) {
        stack<string> st;
        
        for(int i = 0; i < exp.size(); i++) {
            if((exp[i] >= 'A' && exp[i] <= 'Z') ||
            (exp[i] >= 'a' && exp[i] <= 'z') ||
            (exp[i] >= '0' && exp[i] <= '9')) {
                st.push(string(1, exp[i]));
            } else {
                string op1 = st.top();
                st.pop();
                
                string op2 = st.top();
                st.pop();
                
                
                string newOp = "(" + op2 + exp[i] + op1 + ")";
                
                st.push(newOp);
            }
        }
        
        return st.top();
    }
};
```


|     **Time Complexity**      | **Space Complexity** |
| :--------------------------: | :------------------: |
| $O(N) + O(N)$, Adding string |        $O(N)$        |



# References

[[Prefix, Infix and Postfix Conversions]]