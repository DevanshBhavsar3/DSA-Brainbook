14-09-2025  15:01

Status: #Revision-02 

Tags: [[Tags/DSA|DSA]] [[Sliding Window & Two Pointers Problems]]

# Longest Substring Without Repeating Characters

https://leetcode.com/problems/longest-substring-without-repeating-characters/

### Brute Force

- Generate all the substring without duplicates.
- Use a 256 sized array for hashing.

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int longest = 0;
        
        for(int i = 0; i < s.size(); i++) {
            vector<int> arr(256, 0);
            
            for(int j = i; j < s.size(); j++) {
                if(arr[s[j]] == 1) {
                    break;
                }
                
                longest = max(longest, j - i + 1);
                arr[s[j]] = 1;
            }
        }
        
        return longest;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |       $O(256)$       |


### Optimal

- Create 2 pointer left and right.
- Hash every element with its index.
- If the current element is in the hash & it's index is inside the window, move the left to previous occurrence's index + 1.

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> hash(256, -1);
        
        int longest = 0;
        
        int left = 0;
        int right = 0;
        
        while(right < s.size()) {
            // In the map & in the window
            if(hash[s[right]] != -1 && hash[s[right]] >= left) {
                left = hash[s[right]] + 1;
            }
            
            longest = max(longest, right - left + 1);
            hash[s[right]] = right;
            right++;
        }
        
        return longest;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |       $O(256)$       |





# References