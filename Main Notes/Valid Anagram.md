11-11-2025  15:47

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Valid Anagram

https://leetcode.com/problems/valid-anagram/

### Brute Force

- Sort both the string.
- Check if both of them are equal.

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.size() != t.size()) {
            return false;
        }
		
        sort(s.begin(), s.end());
        sort(t.begin(), t.end());
		
        for(int i = 0; i < s.size(); i++) {
            if(s[i] != t[i]) {
                return false;
            }
        }
		
        return true;
    }
};
```

|    **Time Complexity**     | **Space Complexity** |
| :------------------------: | :------------------: |
| $O(2 * (N \log N)) + O(N)$ |        $O(1)$        |


### Optimal

- Hash all the chars of s to the map.
- If hash contains 0 for any char in t, return false.

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.size() != t.size()) {
            return false;
        }
		
        int mp[26];
		
        for(int i = 0; i < s.size(); i++) {
            mp[s[i] - 'a']++;
        }
		
        for(int i = 0; i < t.size(); i++) {
            if(mp[t[i] - 'a'] == 0) {
                return false;
            }
			
            mp[t[i] - 'a']--;
        }
		
        return true;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |       $O(26)$        |





# References