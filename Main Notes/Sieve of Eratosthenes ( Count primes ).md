27-07-2025  15:10

Status: #Revision-02  

Tags: [[Tags/DSA]] [[Advanced Maths]]

# Sieve of Eratosthenes ( Count primes )

https://leetcode.com/problems/count-primes/description/


## Brute Force

- Loop from 2 to N.
- If the i is prime add it to ans.

```cpp
for(i = 2 -> n) {
	if(isPrime(i)) {
		ans.add(i);
	}
}
```


| **Time Complexity** |   **Space Complexity**   |
| :-----------------: | :----------------------: |
|  $O(N * \sqrt n)$   | $O(x)$, x = total primes |



## Optimal

```
N = 10

2 3 4 5 6 7 8 9 10
1 1 1 1 1 1 1 1 1

2 3 4 5 6 7 8 9 10
1 1 0 1 0 1 0 0 0
```


- Create an array of n size.
- Mark every element as 1.
- Loop from 2 to $\sqrt n$, if the prime[i] is 1 mark every multiple of i to 0.
- Loop through 2 to n, and if the prime[i] is 1 increase the count.


```cpp
class Solution {
public:
    int countPrimes(int n) {
        int prime[n + 1];
		
        for(int i = 2; i < n; i++) {
            prime[i] = 1;
        }
		
        for(int i = 2; i * i < n; i++) { // sqrt n because the inner loop starts                                             from i * i
            if(prime[i] == 1) {
                for(int j = i * i; j < n; j += i) {
                    prime[j] = 0;
                }
            }
        }
		
        int cnt = 0;
		
        for(int i = 2; i < n; i++) {
            if(prime[i] == 1) {
                cnt++;
            }
        }
		
        return cnt;
    }
};
```


|        **Time Complexity**        | **Space Complexity** |
| :-------------------------------: | :------------------: |
| $O(N) + O(N \log(\log N)) + O(N)$ |        $O(N)$        |





# References