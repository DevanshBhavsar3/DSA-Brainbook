14-03-2026  17:02

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Minimum Insertion Steps to Make a String Palindrome

https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/

- Find the longest palindromic subsequence.
- The remaining characters will need to be inserted to make the string palindrome.

```cpp
class Solution {
public:
    int lcs(string& s1, string& s2) {
        int n = s1.size();
        int m = s2.size();
		
        vector<int> prev(m + 1);
		
        for(int i = 1; i <= n; i++) {
            vector<int> curr(m + 1);
			
            for(int j = 1; j <= m; j++) {
                if(s1[i - 1] == s2[j - 1]) {
                    curr[j] = 1 + prev[j - 1];
                } else {
                    curr[j] = max(
                        curr[j - 1],
                        prev[j]
                    );
                }
            }
			
            prev = curr;
        }
		
        return prev[m];
    }
	
    int minInsertions(string s) {
        string s2 = s;
        reverse(s2.begin(), s2.end());
		
        return s.size() - lcs(s, s2);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*N)$       |        $O(N)$        |





# References
[[Longest Palindromic Subsequence]]