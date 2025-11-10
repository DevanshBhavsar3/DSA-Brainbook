10-11-2025  15:45

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Reverse Words in a String

https://leetcode.com/problems/reverse-words-in-a-string/

### Brute Force

- Store every word in the stack.
- Create an ans string from the stack.

```cpp
class Solution {
public:
    string reverseWords(string s) {
        stack<string> st;
		
        string word = "";
		
        for(int i = 0; i < s.size(); i++) {
            if(s[i] == ' ') {
                if(!word.empty()) {
                    st.push(word);
                    word = "";
                }
            } else {
                word += s[i];
            }
        }
		
        if(!word.empty()) {
            st.push(word);
        }
		
        string ans = "";
		
        while(st.size() != 1) {
            ans += st.top() + ' ';
            st.pop();
        }
		
        ans += st.top();
        
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |


### Optimal

- Store the words in some tmp variable.
- Whenever new word is found add it to the start of the ans.

```cpp
class Solution {
public:
    string reverseWords(string s) {
        s += " "; // To add the last word
		
        string ans = "";
        int i = 0;
		
        string word = "";
		
        while(i < s.size()) {
            if(s[i] == ' ') {
                if(!word.empty()) {
                    if(ans.empty()) {
                        ans = word;
                    } else {
                        ans = word + " " + ans;
                    }
					
                    word = "";
                }
            } else {
                word += s[i];
            }
			
            i++;
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References