15-09-2025  19:56

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Sliding Window & Two Pointers Problems]]

# Longest Repeating Character Replacement

https://leetcode.com/problems/longest-repeating-character-replacement/

### Brute Force

- Find the substring with k diff elements. ( i.e. substring size - most frequent element )
- Keep track of the maximum element in substring to know the valid substring with at most k changes.

```cpp
class Solution {
public:
    int characterReplacement(string s, int k) {
        int longest = 0;
        
        for(int i = 0; i < s.size(); i++) {
            vector<int> hash(26, 0);
            int maxEl = 0;
            
            for(int j = i; j < s.size(); j++) {
                hash[s[j] - 'A']++;
                
                maxEl = max(maxEl, hash[s[j] - 'A']);
                
                if((j - i + 1) - maxEl <= k) {
                    longest = max(longest, j - i + 1);
                }
            }
        }
        
        return longest;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |     $O(N * 26)$      |


### Better

- Create a sliding window with at most k changes. ( i.e. Window size - most frequent element )
- If changes > k, trim from the left and calculate the most frequent element.

```cpp
class Solution {
public:
    int characterReplacement(string s, int k) {
        vector<int> mp(26, 0);
        int maxFreq = 0;
        
        int left = 0;
        int right = 0;
        
        int longest = 0;
        
        while(right < s.size()) {
            mp[s[right] - 'A']++;
            maxFreq = max(maxFreq, mp[s[right] - 'A']);
            
            while(((right - left + 1) - maxFreq) > k) {
                mp[s[left] - 'A']--;
                
                maxFreq = 0;
                for(int i = 0; i < mp.size(); i++) {
                    maxFreq = max(maxFreq, mp[i]);
                }
                
                left++;
            }
            
            int changes = (right - left + 1) - maxFreq;
            
            if(changes <= k) {
                longest = max(longest, right - left + 1);
            }
            
            right++;
        }
        
        return longest;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(2N * 26)$     |       $O(26)$        |


### Optimal

- Create a sliding window with at most k changes. ( i.e. Window size - most frequent element )
- If changes > k, move left. ( no need to find the new maxFreq ).
- Only update the ans, if the changes are <= k.

> You don't need to find the new maxFreq because,
> 
> changes = size - most frequent number.
> 
> You need to increase the most frequent number not decrease it to get the new max answer.
> Finding the new maxFreq will always result in <= count.

```cpp
class Solution {
public:
    int characterReplacement(string s, int k) {
        vector<int> hash(26, 0);
        int maxFreq = 0;
        
        int left = 0;
        int right = 0;
        
        int longest = 0;
        
        while(right < s.size()) {
            hash[s[right] - 'A']++;
            maxFreq = max(maxFreq, hash[s[right] - 'A']);
            
            if(((right - left + 1) - maxFreq) > k) {
                hash[s[left] - 'A']--;
                left++;
            }
            
            if(((right - left + 1) - maxFreq) <= k) {
                longest = max(longest, right - left + 1);
            }
            
            right++;            
        }
        
        return longest;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |       $O(26)$        |





# References