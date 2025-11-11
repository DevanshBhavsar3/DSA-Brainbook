11-11-2025  15:04

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Isomorphic Strings

https://leetcode.com/problems/isomorphic-strings/

- Create a map to store the last seen index.
- Hash characters from both strings to their maps.
- If both character are not last seen at the same index, return false.

```cpp
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        if(s.size() != t.size()) {
            return false;
        }
		
        map<char, int> mp1;
        map<char, int> mp2;
		
        for(int i = 0; i < s.size(); i++) {
            if(mp1[s[i]] != mp2[t[i]]) {
                return false;
            }
			
            mp1[s[i]] = i + 1;
            mp2[t[i]] = i + 1;
        }
		
        return true;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        | $O(2N) \approx O(1)$ |
> $O(1)$ because you can use 2 256 size arrays.




# References