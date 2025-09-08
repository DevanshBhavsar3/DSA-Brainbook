26-07-2025  15:35

Status: #Revision 

Tags: [[Tags/DSA]] [[Advanced Maths]]

# Print prime factor of a number


## Brute Force

- Loop from 2 till n.
- Check if it is the divisor of n.
- If it check it is a prime no. or not.


```cpp
bool prime(int n) {
	int cnt = 0;
	
	for(int i = 1; i * i < n; i++) {
		if(n % i == 0) {
			cnt++;
			
			if(n / i != i) {
				cnt++;
			}
		}
		if(cnt > 2) return false;
	}
	
	return true;
}

vector<int> primeFactors(int n) {
	vector<int> ans;
	
	for(int i = 2; i < n; i++) {
		if(n % i == 0) {
			if(prime(i)) {
				ans.push_back(i);
			}
		}
	}
	
	return ans;
}
```


| **Time Complexity** | **Space Complexity**      |
| ------------------- | ------------------------- |
| $O(N) * O(\sqrt n)$ | $O(x)$, x = prime factors |



## Better

- Instead of looping till n, loop till $\sqrt n$.
- If the n is divisible by i and is prime add it to ans.
- If n / i != i and prime, add it to ans.


```cpp
bool prime(int n) {
	int cnt = 0;
	
	for(int i = 1; i * i < n; i++) {
		if(n % i == 0) {
			cnt++;
			
			if(n / i != i) {
				cnt++;
			}
		}
		if(cnt > 2) return false;
	}
	
	return true;
}

vector<int> primeFactors(int n) {
	vector<int> ans;
	
	for(int i = 2; i * i < n; i++) {
		if(n % i == 0) {
			if(prime(i)) {
				ans.push_back(i);
			}
			
			if(n / i != i) {
				if(prime(n / i)) {
					ans.push_back(n / i);
				}
			}
		}
	}
	
	return ans;
}
```


| **Time Complexity**           | **Space Complexity**      |
| ----------------------------- | ------------------------- |
| $O(\sqrt n) * O(2 * \sqrt n)$ | $O(x)$, x = prime factors |



## Optimal

```
N = 780

2  | 780
2  | 390
3  | 195
5  | 65
13 | 13
   | 1

```

- Loop till $\sqrt n$.
- if i is divisor of n, add it to ans.
- Divide n till it is no more divisible by i.
- At the end, if the n is not 1 (i.e, prime number like 37), add it to ans.

```cpp
vector<int> primeFactors(int n) {
	vector<int> ans;
	
	for(int i = 2; i * i <= n; i++) {
		if(n % i == 0) {
			ans.push_back(i);
			
			while(n % i == 0) {
				n = n / i;
			}
		}
	}

	// when n is 13
	if(n != 1) ans.push_back(n);
	
	return ans;
}
```


| **Time Complexity**      | **Space Complexity**      |
| ------------------------ | ------------------------- |
| $O(\sqrt n) * O(\log n)$ | $O(x)$, x = prime factors |





# References

[[Divisors of number]]