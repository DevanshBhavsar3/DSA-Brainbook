26-07-2025  16:33

Status: #Revision-03  

Tags: [[Tags/DSA]] [[Advanced Maths]]

# Divisors of number


## Brute Force

- Loop from 1 to N.
- If n is divisible by i, add it to ans.

```cpp
vector<int> divisors(int n) {
	vector<int> ans;
	
	for(int i = 1; i < n; i++) {
		if(n % i == 0) {
			ans.push_back(i);
		}
	}
	
	return ans;
}
```


| **Time Complexity** | **Space Complexity**       |
| ------------------- | -------------------------- |
| $O(N)$              | $O(x)$, x = total divisors |



## Optimal

- Instead of looping till n, loop till $\sqrt n$.
- If n is divisible i, and n / i, add it to ans.

```cpp
vector<int> divisors(int n) {
	vector<int> ans;
	
	for(int i = 1; i * i <= n; i++) {
		if(n % i == 0) {
			ans.push_back(i);
			
			// For cases like 36 / 6 != 6
			if(n / i != i) {
				ans.push_back(n / i);
			}
		}
	}
	
	return ans;
}
```


| **Time Complexity** |    **Space Complexity**    |
| :-----------------: | :------------------------: |
|    $O(\sqrt N)$     | $O(x)$, x = total divisors |





# References