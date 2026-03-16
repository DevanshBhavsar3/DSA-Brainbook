15-03-2026  16:32

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Edit Distance

https://leetcode.com/problems/edit-distance/

## Memoization

- The indices will represent the minimum number of operations required to convert `word1 [0..i]` to `word2 [0..j]`.
- If the character from both the words are matching just skip it.
- Else try all possible operations like,
	- Delete the character (`i - 1`)
	- Replace the character with matching character (`i - 1, j - 1`)
	- Insert new matching character (`i, j - 1`)
	 And return the minimum of them.
- Memoize the indices of the strings.

```cpp
class Solution {
public:
    int find(int i, int j, string& word1, string& word2, vector<vector<int>>& dp) {
        if(j < 0) {
            return i + 1;
        } else if(i < 0) {
            return j + 1;
        }
		
        if(dp[i][j] != -1) {
            return dp[i][j];
        }
		
        if(word1[i] == word2[j]) {
            return dp[i][j] = find(i - 1, j - 1, word1, word2, dp);
        } else {
            int mini = INT_MAX;
			
            // Delete a character
            mini = min(mini, find(i - 1, j, word1, word2, dp));
			
            // Replace a character
            mini = min(mini, find(i - 1, j - 1, word1, word2, dp));
			
            // Insert a character
            mini = min(mini, find(i, j - 1, word1, word2, dp));
			
            return dp[i][j] = mini + 1;
        }
    }
	
    int minDistance(string word1, string word2) {
        int n = word1.size();
        int m = word2.size();
		
        vector<vector<int>> dp(n, vector<int>(m, -1));
		
        return find(n - 1, m - 1, word1, word2, dp);
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
    int minDistance(string word1, string word2) {
        int n = word1.size();
        int m = word2.size();
		
        vector<vector<int>> dp(n + 1, vector<int>(m + 1));
		
        for(int i = 1; i <= n; i++) {
            dp[i][0] = i;
        }
		
        for(int j = 1; j <= m; j++) {
            dp[0][j] = j;
        }
		
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= m; j++) {
                if(word1[i - 1] == word2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    int mini = INT_MAX;
					
                    // Delete a character
                    mini = min(mini, dp[i - 1][j]);
					
                    // Replace a character
                    mini = min(mini, dp[i - 1][j - 1]);
					
                    // Insert a character
                    mini = min(mini, dp[i][j - 1]);
					
                    dp[i][j] = mini + 1;
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
    int minDistance(string word1, string word2) {
        int n = word1.size();
        int m = word2.size();
		
        vector<int> prev(m + 1), curr(m + 1);
		
        for(int j = 1; j <= m; j++) {
            prev[j] = j;
        }
		
        for(int i = 1; i <= n; i++) {
            curr[0] = i;
			
            for(int j = 1; j <= m; j++) {
				
                if(word1[i - 1] == word2[j - 1]) {
                    curr[j] = prev[j - 1];
                } else {
                    int mini = INT_MAX;
					
                    // Delete a character
                    mini = min(mini, prev[j]);
					
                    // Replace a character
                    mini = min(mini, prev[j - 1]);
					
                    // Insert a character
                    mini = min(mini, curr[j - 1]);
					
                    curr[j] = mini + 1;
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