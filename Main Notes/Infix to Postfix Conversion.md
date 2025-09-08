01-08-2025  16:02

Status: #Revision 

Tags: [[Tags/DSA]] [[Stack]]

# Infix to Postfix Conversion

https://www.naukri.com/code360/problems/day-23-:-infix-to-postfix-_1382146


- Iterate over all the char of infix expression.
	- If it is operand, add it to ans.
	- If it is (, add it to stack.
	- If it is ), add everything till ( to ans from stack.
	- Else, add everything with > priority than current operator to ans, and add the operator to stack.
- At last, add remaining operators to ans from stack.


```cpp
#include <bits/stdc++.h>

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

string infixToPostfix(string exp){
	stack<char> st;
	string ans = "";

	for(int i = 0; i < exp.size(); i++) {
		if((exp[i] >= 'A' && exp[i] <= 'Z') ||
		(exp[i] >= 'a' && exp[i] <= 'z') ||
		(exp[i] >= '0' && exp[i] <= '9')) {
			ans += exp[i];
		} else if(exp[i] == '(') {
			st.push(exp[i]);
		} else if(exp[i] == ')') {
			while(!st.empty() && st.top() != '(') {
				ans += st.top();
				st.pop();
			}

			if(st.top() == '(') {
				st.pop();
			}
		} else {
			while(!st.empty() && priority(exp[i]) <= priority(st.top())) {
				ans += st.top();
				st.pop();
			}

			st.push(exp[i]);
		}
	}

	while(!st.empty()) {
		ans += st.top();
		st.pop();
	}

	return ans;
}
```


| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N) + O(N)$    |    $O(N) + O(N)$     |





# References

[[Prefix, Infix and Postfix Conversions]]