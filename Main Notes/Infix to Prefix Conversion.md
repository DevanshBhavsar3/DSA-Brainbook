01-08-2025  16:38

Status: #Revision-03

Tags: [[Tags/DSA]] [[Stack]]

# Infix to Prefix Conversion

https://www.geeksforgeeks.org/problems/infix-to-prefix-notation/1


1. Reverse the infix expression.
	- Don't forget to change the brackets in the reverse string.
2. Convert it to postfix expression.
	-  If the operator is ^, remove all the operators with >= priority from the stack.
	- Else remove operators with > priority from the stack.
3. Reverse the postfix expression.


```cpp
class Solution {
  public:
    int priority(char s) {
        if(s == '^') {
            return 3;
        } else if(s == '*' || s == '/') {
            return 2;
        } else if(s == '+' || s == '-') {
            return 1;
        }
        
        return 0;
    }
	
    string infixToPostfix(string s) {
        stack<char> st;
        string ans;
        
        for(int i = 0; i < s.size(); i++) {
            if((s[i] >= 'A' && s[i] <= 'Z') || 
            (s[i] >= 'a' && s[i] <= 'z') || 
            (s[i] >= '0' && s[i] <= '9')) {
                ans += s[i];
            } else if(s[i] == '(') {
                st.push(s[i]);
            } else if(s[i] == ')') {
                while(!st.empty() && st.top() != '(') {
                    ans += st.top();
                    st.pop();
                }
                
                if(!st.empty() && st.top() == '(') {
                    st.pop();
                }
            } else {
                if(s[i] == '^') {
                    while(!st.empty() && priority(s[i]) <= priority(st.top())) {
                        ans += st.top();
                        st.pop();
                    }    
                } else {
                    while(!st.empty() && priority(s[i]) < priority(st.top())) {
                        ans += st.top();
                        st.pop();
                    }    
                }
                
                
                st.push(s[i]);
            }
        }
        
        while(!st.empty()) {
            ans += st.top();
            st.pop();
        }
        
        return ans;
    }
	
    string infixToPrefix(string s) {
        reverse(s.begin(), s.end());
        
        for(int i = 0; i < s.size(); i++) {
            if(s[i] == '(') {
                s[i] = ')';
            } else if(s[i] == ')') {
                s[i] = '(';
            }
        }
        
        string post = infixToPostfix(s);
        
        reverse(post.begin(), post.end());
        
        return post;
    }
};
```


|               **Time Complexity**                | **Space Complexity** |
| :----------------------------------------------: | :------------------: |
| $O(N / 2) + O(2N) + O(N / 2)$<br>$or$<br>$O(3N)$ |    $O(N) + O(N)$     |





# References

[[Prefix, Infix and Postfix Conversions]]
[[Infix to Postfix Conversion]]