14-11-2025  15:21

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Roman to Integer

https://leetcode.com/problems/roman-to-integer/

- Create a map to store the roman integers with their values.
- If the current char is > next one, add the value to total.
- Else subtract the current value from total.

```cpp
class Solution {
public:
    int romanToInt(string s) {
        map<char, int> mp = {
            {'I', 1},
            {'V', 5},
            {'X', 10},
            {'L', 50},
            {'C', 100},
            {'D', 500},
            {'M', 1000},
        };
		
        int total = 0;
		
        for(int i = 0; i < s.size() - 1; i++) {
            if(mp[s[i]] < mp[s[i + 1]]) {
                total -= mp[s[i]];
            } else {
                total += mp[s[i]];
            }
        }
		
        return total + mp[s.back()];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References