18-11-2025  15:20

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Longest Palindromic Substring

https://leetcode.com/problems/longest-palindromic-substring/

- Consider every index as the center of palindrome string.
- Find the longest string by expanding from the center.

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int start = 0;
        int end = 0;
		
        for(int i = 0; i < s.size(); i++) {
            int oddLen = palindromeLength(s, i, i);
            int evenLen = palindromeLength(s, i, i + 1);
			
            int len = max(oddLen, evenLen);
			
            if(len > (end - start)) {
                start = i - (len - 1) / 2;
                end = i + (len / 2);
            }
        }
		
        return s.substr(start, end - start + 1);
    }
	
    int palindromeLength(string s, int start, int end) {
        while(start >= 0 && end < s.size() && s[start] == s[end]) {
            start--;
            end++;
        }
		
        return end - start - 1;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(1)$        |





# References