13-03-2026  16:07

Status: #Revision-02

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Longest Palindromic Subsequence

https://leetcode.com/problems/longest-palindromic-subsequence/

- Find the longest common subsequence from the string and its reverse.
- The common subsequences between the string and its reversed version will always be palindromes.

```cpp
class Solution {
public:
    int findLCS(string s1, string s2) {
        int n = s1.size();
        int m = s2.size();
		
        vector<int> prev(m + 1);
		
        for(int i = 1; i <= n; i++) {
            vector<int> curr(m + 1);
			
            for(int j = 1; j <= m; j++) {
                if(s1[i - 1] == s2[j - 1]) {
                    curr[j] = prev[j - 1] + 1;
                } else {
                    curr[j] = max(
                        prev[j],
                        curr[j - 1]
                    );
                }
            }
			
            prev = curr;
        }
		
        return prev[m];
    }
	
    int longestPalindromeSubseq(string s) {
        string str = s;
        reverse(str.begin(), str.end());
		
        return findLCS(s, str);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*N)$       |        $O(N)$        |





# References
[[Longest Common Subsequence]]