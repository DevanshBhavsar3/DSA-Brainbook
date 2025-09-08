28-07-2025  16:00

Status: #Revision 

Tags: [[Tags/DSA]] [[Advanced Maths]]

# Pow(x, n)

https://leetcode.com/problems/powx-n/


## Brute Force

- Multiply ans N times.

```cpp
for(i = 1 -> n) {
	ans = ans * x;
}
```


| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |


## Optimal

```
X = 2, N = 21

ans = 1 x 2 x 16 x 65536

X = 2, N = 20  2^10
X = 4, N = 10  (2 * 2)^ 20 / 2
...
X = 65536, N = 1
X = 65536, N = 0
```

- If the pow is odd, remove 1 from the pow and multiply x to ans.
- Else divide the pow by 2 and square the x.

```cpp
class Solution {
public:
    double myPow(double x, int n) {
        double ans = 1;
        long N = n;
		
        if(n < 0) {
            N = -1 * (long) n;
        }
		
        while(N != 0) {
            if(N & 1) {
                ans *= x;
                N -= 1;
            }
			
            x *= x;
            N = N >> 1;
        }
		
        return n < 0 ? (1.0 / ans) : ans;
    }
};
```


| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(\log N)$     |        $O(1)$        |


# References