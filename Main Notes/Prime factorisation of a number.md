27-07-2025  16:25

Status: #Revision-03

Tags: [[Tags/DSA]] [[Advanced Maths]]

# Prime factorisation of a number

https://takeuforward.org/plus/dsa/problems/prime-factorisation-of-a-number

## Brute Force

- For every query, find all the prime factors.

```cpp
class Solution{
    public:
        vector<int> findPrimeFactors(int n) {
            vector<int> ans;
			
            for(int i = 2; i * i <= n; i++) {            
                while(n % i == 0) {
                    ans.push_back(i);
                    n = n / i;
                }
            }
			
            if(n != 1) ans.push_back(n);
			
            return ans;
        }
		
        vector<vector<int>> primeFactors(vector<int>& queries){
            vector<vector<int>> ans;
			
            for(int i = 0; i < queries.size(); i++) {
                vector<int> factors = findPrimeFactors(queries[i]);
                ans.push_back(factors);
            }
			
            return ans;
        }
};
```


|     **Time Complexity**      |           **Space Complexity**           |
| :--------------------------: | :--------------------------------------: |
| $O(q) * O(\sqrt n * \log n)$ | $O(x)$, x = all prime factors of queries |



## Optimal

- Create a Smallest Prime Factor array, with same value as its index.
- For i in spf, if spf[i] is same as its index (i.e, prime), change the multiple of it to the i.
- Divide the query until it becomes 1 with spf[n].


```cpp
class Solution{
    public:
        vector<vector<int>> primeFactors(vector<int>& queries){
            int spf[INT_MAX + 1];
			
			// O(N)
            for(int i = 0; i < INT_MAX; i++) {
                spf[i] = i;
            }
			
			// N log(log N)
            for(int i = 2; i * i < INT_MAX; i++) {
                if(spf[i] == i) {
                    for(int j = i * i; j < INT_MAX; j += i) {
                        if(spf[j] == j) { // Only change if its not changed
                            spf[j] = i;
                        }
                    }
                }
            }
			
            vector<vector<int>> ans;
			
			// O(Q log N)
            for(int i = 0; i < queries.size(); i++) {
                vector<int> factors;
                int n = queries[i];
                
                while(n != 1) {
                    factors.push_back(spf[n]);
                    n /= spf[n];
                }
				
                ans.push_back(factors);
            }
			
            return ans;
        }
};
```


|            **Time Complexity**             |           **Space Complexity**           |
| :----------------------------------------: | :--------------------------------------: |
| $O(N) + O(N \log(\log N)) + O(Q * \log n)$ | $O(x)$, x = all prime factors of queries |





# References

[[Print prime factor of a number]]

[[Sieve of Eratosthenes ( Count primes )]]