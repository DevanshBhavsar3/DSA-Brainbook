20-09-2025  14:46

Status: #Revision-03

Tags: [[Tags/DSA|DSA]] [[Sliding Window & Two Pointers Problems]]

# Minimum Window Substring

https://leetcode.com/problems/minimum-window-substring/

### Brute Force

- Loop through all the substring of s.
- First hash all the elements from t.
- If current char has positive hash ( in the t ), increase the count and decrease the hash value.
- When the count reaches t.size(), it is the minimum valid string.

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        int minLen = INT_MAX;
        int start = -1;
        
        for(int i = 0; i < s.size(); i++) {
            map<char, int> mp;
            
            // Hash every element of t
            for(int j = 0; j < t.size(); j++) {
                mp[t[j]]++;
            }
            
            int cnt = 0;
            
            for(int j = i; j < s.size(); j++) {
                // If the current element in positive in map that means it is in t
                if(mp[s[j]] > 0) {
                    cnt++;
                }
                
                mp[s[j]]--;
                
                // The substring contains all chars from t
                if(cnt == t.size()) {
                    int length = j - i + 1;
                    
                    if(length < minLen) {
                        minLen = j - i + 1;
                        start = i;
                    }
                    
                    break;
                }
            }
        }
        
        if(start == -1) {
            return "";
        }
        
        return s.substr(start, minLen); 
    }
};
```

|               **Time Complexity**               | **Space Complexity** |
| :---------------------------------------------: | :------------------: |
| $O(N * (N + M))$<br><br>Map complexity excluded |       $O(256)$       |


### Optimal

- Hash every element from string t.
- Create a sliding window, if the right element has positive hash ( in the t ), increase the cnt and decrease the hash value.
- While the window is valid ( cnt == t.size() ), remove elements from the left and update the min length.

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        map<char, int> mp;
        
        for(int i = 0; i < t.size(); i++) {
            mp[t[i]]++;
        }
        
        int left = 0;
        int right = 0;
        
        int cnt = 0;
        int start = -1;
        int minLength = INT_MAX;
        
        while(right < s.size()) {
            if(mp[s[right]] > 0) {
                cnt++;
            }
            
            mp[s[right]]--;
            
            while(cnt == t.size()) {
                if((right - left + 1) < minLength) {
                    minLength = right - left + 1;
                    start = left;
                }
                
                mp[s[left]]++;
                
                if(mp[s[left]] > 0) {
                    cnt--;
                }
                
                left++;
            }
            
            right++;
        }
        
        if(start == -1) {
            return "";
        }
        
        return s.substr(start, minLength);
    }
};
```

|             **Time Complexity**             | **Space Complexity** |
| :-----------------------------------------: | :------------------: |
| $O(2N + M)$<br><br>Excluding map complexity |       $O(256)$       |





# References