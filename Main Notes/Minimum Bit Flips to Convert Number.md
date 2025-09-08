24-07-2025  12:47

Status: #Revision-02  

Tags: [[Tags/DSA]] [[Bit Manipulation]]

# Minimum Bit Flips to Convert Number

https://leetcode.com/problems/minimum-bit-flips-to-convert-number/



```
start = 10, goal = 7

  1 0 1 0
^ 0 1 1 1
---------
  1 1 0 1 (Bits to flip)
```


- Find the xor of start and goal, it will be the bits to change.
- Count total no. of set bits in the xor.


```cpp
class Solution {
	public:
	int minBitFlips(int start, int goal) {
		if(start == goal) return 0;
		
		int ans = start ^ goal;
		
		int setBits = 1;
		
		while(ans != 1) {
			setBits += ans & 1;
			ans = ans >> 1;
		}
		
		return setBits;
	}
};
```

| **Time Complexity**            | **Space Complexity** |
| ------------------------------ | -------------------- |
| $O(\log(x))$, x = start ^ goal | $O(1)$               |

# References