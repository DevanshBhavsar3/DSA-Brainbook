18-09-2025  15:18

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Sliding Window & Two Pointers Problems]]

# Number of Substrings Containing All Three Characters

https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/

### Brute Force

- For every substring increase the total if, the substring contains all 3 chars.
- If the current substring contains all 3 chars, then every remaining substring will also be valid substring.

```cpp
class Solution {
public:
    int numberOfSubstrings(string s) {
        int total = 0;
        
        for(int i = 0; i < s.size(); i++) {
            vector<int> hash(3, 0);
            
            for(int j = i; j < s.size(); j++) {
                hash[s[j] - 'a'] = 1;
                
                if(hash[0] == 1 &&
                hash[1] == 1 &&
                hash[2] == 1) {
                    total += s.size() - j;
                    break;
                }
            }
        }    
        
        return total;  
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $ON^2)$       |        $O(1)$        |


### Optimal

- Hash the last seen index of every chars.
- When all of them contains index, add minimum of the window (i.e. min(hash[0], hash[1], hash[2])) + 1 to the total.

```cpp
class Solution {
public:
    int numberOfSubstrings(string s) {
        int hash[] = {-1, -1, -1};
        int total = 0;
        
        for(int i = 0; i < s.size(); i++) {
            hash[s[i] - 'a'] = i;
            // The starting point of the valid minimum window + 1 = total valid substrings
            total += min(hash[0], min(hash[1], hash[2])) + 1;
        }
        
        return total;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References