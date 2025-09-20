19-09-2025  15:16

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Sliding Window & Two Pointers Problems]]

# Longest Substring with At Most K Distinct Characters

https://www.naukri.com/code360/problems/longest-sub-string-with-at-most-k-distinct-characters_699944

### Brute Force

- Iterate over all the substring while hashing the char frequencies.
- If map size is > k, break the loop.

```cpp
#include <bits/stdc++.h>

int getLengthofLongestSubstring(int k, string s) {
	int ans = 0;
	
	for(int i = 0; i < s.size(); i++) {
		map<char, int> mp;
	    
	    for(int j = i; j < s.size(); j++) {
			mp[s[j]]++;
		    
		    if(mp.size() > k) {
			    break;
			}
			
			ans = max(ans, j - i + 1);
	    }
	}
	
	return ans;
}
```

|                                      **Time Complexity**                                       | **Space Complexity** |
| :--------------------------------------------------------------------------------------------: | :------------------: |
| $O(N^2)$ +<br>$O(\log 256)$ (Map), <br><br>$O(256)$ (Unordered Map)<br>$O(256^2)$ (Worst Case) |    $O(256)$ (Map)    |


### Better

- Create a sliding window with at most k distinct chars.
- If distinct chars are > k, move left until 1 char is removed.

```cpp
#include <bits/stdc++.h>

int getLengthofLongestSubstring(int k, string s)
{
	map<char, int> mp;
	
	int left = 0;
	int right = 0;
	
	int ans = 0;
	
	while(right < s.size()) {
	    mp[s[right]]++;
        
	    while(mp.size() > k) {
	        mp[s[left]]--;
	        
	        if(mp[s[left]] == 0) {
	            mp.erase(s[left]);
	        }
	        
	        left++;
	    }
	    
	    ans = max(ans, right - left + 1);
	    
	    right++;
	}
	
	return ans;
}
```

|                                     **Time Complexity**                                     | **Space Complexity** |
| :-----------------------------------------------------------------------------------------: | :------------------: |
| $O(2N)$ +<br>$O(\log 256)$ (Map), <br><br>$O(1)$ (Unordered Map)<br>$O(256^2)$ (Worst Case) |       $O(256)$       |


### Optimal

- Create a sliding window with at most k distinct chars.
- If distinct chars > k, move left.
- Only update the ans, if the distinct chars are <= k.

```cpp
#include <bits/stdc++.h>

int getLengthofLongestSubstring(int k, string s)
{
	map<char, int> mp;
	
	int left = 0;
	int right = 0;
	
	int ans = 0;
	
	while(right < s.size()) {
		mp[s[right]]++;
		
	    if(mp.size() > k) {
	        mp[s[left]]--;
	        
	        if(mp[s[left]] == 0) {
		        mp.erase(s[left]);
	        }
	        
	        left++;
	    }
	    
	    if(mp.size() <= k) {
	        ans = max(ans, right - left + 1);
	    }
	    
	    right++;
	}
	
	return ans;
}

```

|                                    **Time Complexity**                                     | **Space Complexity** |
| :----------------------------------------------------------------------------------------: | :------------------: |
| $O(N)$ +<br>$O(\log 256)$ (Map), <br><br>$O(1)$ (Unordered Map)<br>$O(256^2)$ (Worst Case) |       $O(256)$       |





# References