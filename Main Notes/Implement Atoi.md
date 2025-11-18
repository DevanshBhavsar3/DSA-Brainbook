18-11-2025  14:47

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Implement Atoi

https://leetcode.com/problems/string-to-integer-atoi/

- Remove leading zeros.
- Store the sign if present.
- Iterate until non-digit character while storing it in the res.
- If anytime the ans is outside INT boundary return boundary value.

```cpp
class Solution {
public:
    int myAtoi(string s) {
        int i = 0;
		
        while(i < s.size() && s[i] == ' ') {
            i++;
        }
		
        int sign = 0;
		
        if(s[i] == '-') {
            sign = 1;
            i++;
        } else if(s[i] == '+') {
            sign = 0;
            i++;
        }
		
        long ans = 0;
		
        while(i < s.size() && isdigit(s[i])) {
            int digit = s[i] - '0';
			
            ans = (ans * 10) + digit;
            i++;
			
            if(ans > INT_MAX) {
                return sign ? INT_MIN : INT_MAX;
            }
        }
		
        ans = sign ? -ans: ans;
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References