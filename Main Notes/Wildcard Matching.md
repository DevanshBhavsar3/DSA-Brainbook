16-03-2026  15:45

Status: #Revision-02

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Wildcard Matching

https://leetcode.com/problems/wildcard-matching/

## Memoization

- The indices will represent if the `s [0..i]` and `j [0..j]` are matching or not.
- If the character from both the words are matching just skip it.
- Else try all possible operations like,
	- Matching `?` (`i - 1, j - 1`)
	- Matching `*` (`i - 1, j` || `i, j - 1`)
- If the `p` is exhausted, `s` should be also be exhausted.
- If the `s` is exhausted, `p` should only contains `*`s.
- Memoize the indices of the strings.

```cpp
class Solution {
public:
    bool match(int i, int j, string& s, string& p, vector<vector<int>>& dp) {
        if(j < 0) {
            return i < 0;
        } else if(i < 0) {
            for(int idx = j; idx >= 0; idx--) {
                if(p[idx] != '*') {
                    return false;
                }
            }
			
			return true;
        }
		
        if(dp[i][j] != -1) {
            return dp[i][j];
        }
		
        if(s[i] == p[j] || p[j] == '?') {
            return dp[i][j] = match(i - 1, j - 1, s, p, dp);
        } else if(p[j] == '*') {
            return dp[i][j] = match(i, j - 1, s, p, dp) || match(i - 1, j, s, p, dp);
        }
		
        return dp[i][j] = false;
    }
	
    bool isMatch(string s, string p) {
        int n = s.size();
        int m = p.size();
		
        vector<vector<int>> dp(n, vector<int>(m, -1));
		
        return match(n - 1, m - 1, s, p, dp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*M)$       |  $O(N*M) + O(N+M)$   |


## Tabulation

```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int n = s.size();
        int m = p.size();
		
        vector<vector<bool>> dp(n + 1, vector<bool>(m + 1, false));
		
        dp[0][0] = true;
		
        bool onlyStars = true;
		
        for(int j = 1; j <= m; j++) {
            if(p[j - 1] != '*') {
                onlyStars = false;
            }
			
            dp[0][j] = onlyStars;
        }
		
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= m; j++) {
                if(s[i - 1] == p[j - 1] || p[j - 1] == '?') {
                    dp[i][j] = dp[i - 1][j - 1];
                } else if(p[j - 1] == '*') {
                    dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
                } else {
                    dp[i][j] = false;
                }
            }
        }
		
        return dp[n][m];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*M)$       |       $O(N*M)$       |
### Space Optimization

```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int n = s.size();
        int m = p.size();
		
        vector<bool> prev(m + 1, false);
        prev[0] = true;
		
        bool onlyStars = true;
		
        for(int j = 1; j <= m; j++) {
            if(p[j - 1] != '*') {
                onlyStars = false;
            }
			
            prev[j] = onlyStars;
        }
		
        for(int i = 1; i <= n; i++) {
            vector<bool> curr(m + 1, false);
			
            for(int j = 1; j <= m; j++) {
                if(s[i - 1] == p[j - 1] || p[j - 1] == '?') {
                    curr[j] = prev[j - 1];
                } else if(p[j - 1] == '*') {
                    curr[j] = curr[j - 1] || prev[j];
                } else {
                    curr[j] = false;
                }
            }
			
            prev = curr;
        }
		
        return prev[m];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*M)$       |        $O(M)$        |





# References