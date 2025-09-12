01-08-2025  17:16

Status: #Revision-02 

Tags: [[Tags/DSA]] [[Stack]]

# Prefix to Infix Conversion

https://www.naukri.com/code360/problems/prefix-to-infix_1215000


- Start iterating prefix expression from back.
- If it is an operand add it to ans.
- Else, get the last 2 operands and put the operator in between and cover them in brackets.

```cpp
string prefixToInfixConversion(string &s){
	stack<string> st;
	
	for(int i = (s.size() - 1); i >= 0; i--) {
		if((s[i] >= 'A' && s[i] <= 'Z') ||
		(s[i] >= 'a' && s[i] <= 'z') || 
		(s[i] >= '0' && s[i] <= '9')) {
			st.push(string(1, s[i]));
		} else {
			string op1 = st.top();
			st.pop();
			
			string op2 = st.top();
			st.pop();
			
			string newOp = '(' + op1 + s[i] + op2 + ')';
			
			st.push(newOp);
		}
	}
	
	return st.top();
}
```


|     **Time Complexity**      | **Space Complexity** |
| :--------------------------: | :------------------: |
| $O(N) + O(N)$, Adding string |        $O(N)$        |





# References

[[Prefix, Infix and Postfix Conversions]]