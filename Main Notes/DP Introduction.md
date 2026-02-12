08-02-2026  16:26

Status:

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# DP Introduction

## Memoization (Top Down)

Store the results of subproblems and use them to solve similar subproblems.

This is called **Top Down** approach because, using recursion you start from the main problem, then recurse until the base case and again come back.

Example,
In Fibonacci series, store the result of every index in an array and use that array to return answers for the same index in further calls.

```cpp
#include <bits/stdc++.h>
using namespace std;

// Total function call O(N)
int fib(int n, int dp[]) {
    if(n <= 1) {
        return n;
    }
	
    if(dp[n] != -1) {
        return dp[n];
    }
	
    return dp[n] = fib(n - 1, dp) + fib(n - 2, dp);
}

int main(void) {
    int n;
    cin >> n;
	
    int dp[n + 1];
    memset(dp, -1, sizeof(dp));
	
    cout << fib(n, dp) << endl;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |       $O(2N)$        |


## Tabulation (Bottom Up)

This is called **Bottom Up** approach because, you start from the base case then go the main problem.

Example,
In Fibonacci series, store the base cases in a dp array, start from the 2nd index till n and calculate the result.

```cpp
#include <bits/stdc++.h>
using namespace std;

int fib(int n) {
    vector<int> dp(n + 1);
	
    dp[0] = 0;
    dp[1] = 1;
	
    for(int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
	
    return dp[n];
}

int main(void) {
    int n;
    cin >> n;
	
    cout << fib(n) << endl;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |


## Space Optimization

We only need to store the previous 2 element in order to calculate the current Fibonacci number. So we can optimize the space by storing only 2 variables instead of entire array. 

```cpp
#include <bits/stdc++.h>
using namespace std;

int fib(int n) {
    vector<int> dp(2);
	
    dp[0] = 0;
    dp[1] = 1;
	
    for(int i = 2; i <= n; i++) {
        int curr = dp[0] + dp[1];
		
        dp[0] = dp[1]; 
        dp[1] = curr;
    }
	
    return dp[1];
}

int main(void) {
    int n;
    cin >> n;
	
    cout << fib(n) << endl;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References