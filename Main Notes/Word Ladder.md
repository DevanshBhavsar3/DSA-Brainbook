11-12-2025  15:58

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Word Ladder

https://leetcode.com/problems/word-ladder/

- Create a set from the word list.
- Perform BFS, which changes every letter of word from "a" to "z".
- If that word is in the set, add it to the queue with its level and remove that word from the set.
- Anytime the end word is encountered, return the level.

```cpp
class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        set<string> dict(wordList.begin(), wordList.end());
        queue<pair<string, int>> q;
        
        q.push({beginWord, 1});
        dict.erase(beginWord);
		
		// O(N) - Only word that are in the set will be added to the queue
        while(!q.empty()) {
            pair<string, int> top = q.front();
            q.pop();
			
            string word = top.first;
            int level = top.second;
			
            if(word == endWord) {
                return level;
            }
			
			// O(Word length * 26)
            for(int i = 0; i < word.size(); i++) {
                char original = word[i];
				
                for(char j = 'a'; j <= 'z'; j++) {
                    word[i] = j;
                    
                    if(dict.find(word) != dict.end()) {
                        q.push({word, level + 1});
                        dict.erase(word);
                    }    
                }
                
                word[i] = original;
            }
        }
		
        return 0;
    }
};
```

|       **Time Complexity**        | **Space Complexity** |
| :------------------------------: | :------------------: |
| $O(N * x * 26)$, x = word length |       $O(2N)$        |





# References