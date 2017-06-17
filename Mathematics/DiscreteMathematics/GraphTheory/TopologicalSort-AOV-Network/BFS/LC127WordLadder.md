# 127. Word Ladder

### LeetCode

## Question

Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

1.  Only one letter can be changed at a time.
2.  Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

**For example,**

**Given:**
```
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log","cog"]
```

**Result:**
```
As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.
```

**Note:**

* Return 0 if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume beginWord and endWord are non-empty and are not the same.

**UPDATE (2017/1/20):**

`The wordList parameter had been changed to a list of strings (instead of a set of strings). Please reload the code definition to get the latest changes.`

## Solutions

* C++1
```
int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        //if(wordList.find(endWord) == wordList.end()) return 0;
        unordered_map<string, int> dp;
        for(string word : wordList)
            dp[word] = INT_MAX;
        if(dp.count(endWord)==0) return 0;
        if(beginWord==endWord) return 1;
        dp[endWord] = 1;
        dp[beginWord] = INT_MAX;
        queue<string> q;
        q.push(endWord);
        while(!q.empty())
        {
            string target = q.front();
            q.pop();
            string temp = target;
            for(int i=0; i<target.length(); ++i)
            {
                for(char c='a'; c<='z'; ++c)
                {
                    if(c == target[i]) continue;
                    temp[i] = c;
                    if(dp.count(temp)>0 && dp[temp]==INT_MAX)
                    {
                        dp[temp] = dp[target]+1;
                        q.push(temp);
                    }
                    if(temp==beginWord) return dp[temp];
                }
                temp[i] = target[i];
            }
        }
        return 0;
}
```

* C++2
```
int ladderLength(string beginWord, string endWord, unordered_set<string>& wordList) {
        int res=1;
        //n = wordList.empty() ? 0 : (*wordList.begin()).size();
        unordered_set<string> beginSet {beginWord}, endSet{endWord};
        while(!beginSet.empty())
        {
            res++;
            unordered_set<string> set;
            for(string word : beginSet) wordList.erase(word);
            for(string word : beginSet)
            {
                string next = word;
                for(int i=0; i<word.size(); ++i)
                {
                    for(char c='a'; c<='z'; ++c)
                    {
                        next[i] = c;
                        if(wordList.find(next)==wordList.end()) continue;
                        if(endSet.find(next)!=endSet.end()) return res;
                        set.insert(next);
                    }
                    next[i] = word[i];
                }
            }
            beginSet = set.size()<endSet.size() ? set : endSet;
            endSet = set.size()<endSet.size() ? endSet : set;
        }
        return 0;
    }
```

## Explanation

See the requirements

`1.  Only one letter can be changed at a time.`

Every step just one letter can be changed

`2.  Each transformed word must exist in the word list. Note that beginWord is not a transformed word.`

All words must be in the word list except the **beginWord**.

### Solution C++1

Search from **endWord** to **beginWord**

Use an array `dp` to save the distances from any word in the `wordList` to the **endWord**. The 'dp' is also used to index (INT_MAX means not been visited yet) if the word has been used or not.

Use a Queue to traverse the available changed word.

Question here: is Stack working? (I think it should also work)

**Note:** don't forget to use backtracking to recover the `temp` word

If we found the **beginWord** during the search process, return the `dp` step number

If it's unreachable, return 0.

### Solution C++2

Quite similar idea as above. 

The different is this algorithm can search from **endWord** group or **beginWord** group.

Actually search from a smaller word set to a larger word set, which can save some time.
