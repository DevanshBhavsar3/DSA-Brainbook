20-09-2025  16:27

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Sliding Window & Two Pointers Problems]]

# Minimum Window Subsequence

https://www.naukri.com/code360/problems/minimum-window-subsequence_2181133

- Keep 2 pointers i and j.
- If S[i] == T[j], increase both i and j.
- When j reaches end, loop until the string is constructed backward.
- Update the window size and starting position.

```cpp
string minWindow(string S, string T)
{
	int minLength = INT_MAX;
	int start = -1;
	
	int i = 0;
	int j = 0;
	
	while(i < S.size()) {
		if(S[i] == T[j]) {
			j++;
		}
		
		if(j >= T.size()) {
			int end = i;
			j--;
			
			while(j >= 0) {
				if(S[i] == T[j]) {
					j--;	
				}
				
				i--;
			}
			
			i++;
			j++;
			
			if((end - i + 1) < minLength) {
				minLength = end - i + 1;
				start = i;
			}
		}
		
		i++;
	}
	
	if(start == -1) {
		return "";
	}
	
	return S.substr(start, minLength);
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(1)$        |





# References