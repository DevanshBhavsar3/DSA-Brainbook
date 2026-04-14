12-03-2026  17:07

Status: #Revision-02

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Print Longest Common Subsequence

https://www.naukri.com/code360/problems/print-longest-common-subsequence_8416383

![[Pasted image 20260312173238.png]]

- Generate the dp matrix from the longest common subsequence problem. 
- From index m and n, backtrack till one of the index becomes 0.
- If at any index the char are same, append the char to the ans, and decrease i and j.
- Else travel where the lcs is most.

```cpp
string findLCS(int n, int m,string &s1, string &s2){
	vector<vector<int>> dp(n + 1, vector<int>(m + 1));
	
	for(int i = 0; i <= n; i++) {
		dp[i][0] = 0;
	}
	
	for(int j = 0; j <= m; j++) {
		dp[0][j] = 0;
	}
	
	for(int i = 1; i <= n; i++) {
		for(int j = 1; j <= m; j++) {
			if(s1[i - 1] == s2[j - 1]) {
				dp[i][j] = dp[i - 1][j - 1] + 1;
			} else {
				dp[i][j] = max(
					dp[i][j - 1],
					dp[i - 1][j]
				);
			}
		}
	}
	
	string lcs = "";
	int i = n;
	int j = m;
	
	while(i > 0 && j > 0) {
		if(s1[i - 1] == s2[j - 1]) {
			lcs = s1[i - 1] + lcs;
			
			i--;
			j--;
		} else if(dp[i - 1][j] > dp[i][j - 1]) {
			i--;
		} else {
			j--;
		}
	}
	
	return lcs;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
| $O(N*M) + O(N + M)$ |      $O(N * M)$      |





# References
[[Longest Common Subsequence]]