10-11-2025  16:14

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Largest Odd Number in String

https://leetcode.com/problems/largest-odd-number-in-string/

- Start iterating from the back, until you found the odd digit.
- Return substring till that idx. Else return empty string.

```cpp
class Solution {
public:
    string largestOddNumber(string num) {
        int last = -1;
		
        for(int i = num.size() - 1; i >= 0; i--) {
            if((num[i] - '0') & 1) {
                last = i;
                break;
            }
        }
		
        if(last == -1) {
            return "";
        }
		
        return num.substr(0, last + 1);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References