22-09-2025  15:02

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Valid Parenthesis String

https://leetcode.com/problems/valid-parenthesis-string/

### Brute Force

- If the current char is ( then increase the count, if it is ) then decrease it.
- If it is * , then check for all 3 possibility.

```cpp
class Solution {
public:
    bool checkValidity(string s, int idx, int cnt) {
        if(cnt < 0) {
            return false;
        }
        
        if(idx >= s.size()) {
            return cnt == 0;
        }
        
        if(s[idx] == '(') {
            return checkValidity(s, idx + 1, cnt + 1);
        } else if(s[idx] == ')') {
            return checkValidity(s, idx + 1, cnt - 1);
        }
        
        return checkValidity(s, idx + 1, cnt + 1) || checkValidity(s, idx + 1, cnt - 1) || checkValidity(s, idx + 1, cnt);
    }
    
    bool checkValidString(string s) {
        return checkValidity(s, 0, 0);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(3^N)$       |        $O(N)$        |


### Better

- Add opening brackets and asterisks to its respective stack.
- When ")" occurs, first remove from opening brackets stack if possible, else remove from asterisks.
- Remove all the valid opening and asterisks from the stack.

```cpp
class Solution {
public:
    bool checkValidString(string s) {
        stack<int> openBrackets;
        stack<int> asterisks;
        
        for(int i = 0; i < s.size(); i++) {
            if(s[i] == '(') {
                openBrackets.push(i);
            } else if(s[i] == '*') {
                asterisks.push(i);
            } else {
                if(!openBrackets.empty()) {
                    openBrackets.pop();
                } else if(!asterisks.empty()) {
                    asterisks.pop();
                } else {
                    return false;
                }
            }
        }
        
        while(!openBrackets.empty() && !asterisks.empty()) {
            if(openBrackets.top() > asterisks.top()) {
                return false;
            }
            
            openBrackets.pop();
            asterisks.pop();
        }
        
        // Only check for openBrackets and consider all remaining * as "".
        return openBrackets.empty();
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |        $O(N)$        |


### Optimal

- Iterate from both ends of the string.
- From left if the char is ( or * , increase opening count, else decrease it.
- From right if the char is ) or * , increase closing count, else decrease it.
- Anytime opening count or closing count is < 0, return false.

```cpp
class Solution {
public:
    bool checkValidString(string s) {
        int length = s.size();
        
        int openCount = 0;
        int closeCount = 0;
        
        for(int i = 0; i < length; i++) {
            if(s[i] == '(' || s[i] == '*') {
                openCount++;
            } else {
                openCount--;
            }
            
            if(s[length - i - 1] == ')' || s[length - i - 1] == '*') {
                closeCount++;
            } else {
                closeCount--;
            }
            
            if(openCount < 0 || closeCount < 0) {
                return false;
            }
        }
        
        return true;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References