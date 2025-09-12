10-08-2025  16:35

Status: #Revision-02 

Tags: [[Tags/DSA]] [[Stack]]

# Remove K Digits

https://leetcode.com/problems/remove-k-digits/description/

- Create a monotonic stack of increasing elements.
- While creating only remove K elements from the top.
- Remove any leading 0 from the ans.

> *You can use string instead of stack.*

```cpp
class Solution {
public:
    string removeKdigits(string num, int k) {
        if(num.size() == k) return "0";
		
        string ans = "";
		
        for(int i = 0; i < num.size(); i++) {
            while(!ans.empty() && (k != 0) && (num[i] < ans.back())) {
                ans.pop_back();
                k--;
            }
			
            ans += num[i];
        }
		
        while(k != 0) {
            ans.pop_back();
            k--;
        }
		
        while(!ans.empty() && ans.front() == '0') {
            ans.erase(0, 1);
        }
		
        if(ans.empty()) {
            return "0";
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|   $O(2N) + O(K)$    |        $O(N)$        |





# References

[[Monotonic Stack]]