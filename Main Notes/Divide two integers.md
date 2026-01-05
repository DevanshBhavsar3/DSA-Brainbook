22-07-2025  15:22

Status: #Revision-03

Tags: [[Tags/DSA]] [[Tags/Bit Manipulation|Bit Manipulation]]

# Divide two integers

https://leetcode.com/problems/divide-two-integers/

## Brute Force:

- Add up the divisor until it is <= dividend.

> Doesn't work with negative ans.

```cpp
int ans = 0;

while(ans + divisor <= divident) {
	ans += divisor;
}

return ans;
```

| Time Complexity | Space Complexity |
| :-------------: | :--------------: |
| $O(N)$, N = ans |      $O(1)$      |


## Optimal:

```
dividend = 22
divisor = 3

(3 x 7)

(3 x (4 + 2 + 1))

3 x (2^2 + 2^1 + 2^0)

3 x 2^2
3 x 2^1
3 x 2^0

ans = 7
```

- Subtract the $divisor * 2^x$  from the dividend.
- Where x is the biggest exponent that can be removed.
- Add that bit to the quotient ans.
- Perform everything on positive value, but return the ans as per the given sign.


```cpp
class Solution {
	public:
	int divide(int dividend, int divisor) {
		if(dividend == divisor) {
			return 1;
		}
		
		// Check if one of the given is negative.
		bool sign = false;
		
		if(dividend < 0 && divisor >= 0) {
			sign = true;
		} else if(dividend >= 0 && divisor < 0) {
			sign = true;
		}
		
		// Convert to postive.
		// 2^31 will overflow, so long.
		long n = abs((long) dividend);
		long d = abs((long) divisor);
		
		long ans = 0;
		
		// Log N
		// While the dividend is divisable by divisor
		while(n >= d) {
			int cnt = 0;
			
			// Log N
			// d * 2^cnt + 1 
			while(n >= (d << (cnt + 1))) {
				cnt++;
			}
			
			// 2 ^ cnt
			ans += 1 << cnt;
			
			// d * 2^cnt
			n -= (d << cnt);
		}
		
		// 2^31 with positive no.
		if(ans == (1 << 31) && sign == false) {
			return INT_MAX;
			
		// 2^31 with negative no.
		} else if(ans == (1 << 31) && sign == true) {
			return INT_MIN;
		}
		
		return sign ? -ans : ans;
	}
};
```

| Time Complexity | Space Complexity |
| --------------- | ---------------- |
| $O((\log n)^2)$ | $O(1)$           |





# References 