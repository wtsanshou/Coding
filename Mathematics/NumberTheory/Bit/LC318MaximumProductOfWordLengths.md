# LC318. Maximum Product of Word Lengths

### LeetCode

## Question

Given a string array words, find the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters. You may assume that each word will contain only lower case letters. If no such two words exist, return 0.

**Example 1:**

```
Given ["abcw", "baz", "foo", "bar", "xtfn", "abcdef"]
Return 16
The two words can be "abcw", "xtfn".
```

**Example 2:**

```
Given ["a", "ab", "abc", "d", "cd", "bcd", "abcd"]
Return 4
The two words can be "ab", "cd".
```

**Example 3:**

```
Given ["a", "aa", "aaa", "aaaa"]
Return 0
No such pair of words.
```

## Solutions

### Solution 1

* Java (238 ms  38.5 MB)
```
class Solution {
    public int maxProduct(String[] words) {
        int res = 0;
        
        for(int i=0; i<words.length; i++)
            for(int j=i+1; j<words.length; j++)
                res = Math.max(res, productOf(words[i], words[j]));
            
        return res;
    }
    
    private int productOf(String word1, String word2){
        return shareCommonLetters(word1, word2) ? 0 : word1.length() * word2.length();
    }
    
    private boolean shareCommonLetters(String word1, String word2){
        boolean[] visit = new boolean[128];
        for(char w1 : word1.toCharArray())
            visit[w1] = true;
        
        for(char w2 : word2.toCharArray())
            if(visit[w2]) return true;
        
        return false;
    }
}
```

When I see this question, the most straight forward idea is to compare all possible pair of words in `words`. The key to check if both words share common letters, which can be implement by using a boolean array to memory the letters of `word1` and then check `word2` to see if they have shared common letters.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup> * w), where `n` is the length of the input `words`, `w` is the length of the longest word in the `words`. 
* **worst-case space complexity:** `O(1)`.

### Solution 2

* C++ (69ms) O(mn)
```
int maxProduct(vector<string>& words) {
    unordered_map<int, int> maxLen;
    for(string word : words)
    {
        int mask=0;
        for(char c : word)
        {
            mask |= 1<<(c-'a');
        }
        maxLen[mask] = max(maxLen[mask], (int)word.size());
    }
    int result = 0;
    for(auto a : maxLen)
    {
        for(auto b : maxLen)
        {
            if((a.first & b.first)==0)
            {
                result = max(result, a.second*b.second);
            }
        }
    }
    return result;
}
```

* Java (69ms)
```
public int maxProduct(String[] words) {
    Map<Integer, Integer> map = new HashMap<>();
    int res = 0;
    for(String word : words)
    {
        int mask = 0, len = word.length();
        for(int i=0; i<len; ++i)
        {
            mask |= 1 << (word.charAt(i)-'a');
        }
        int longer = (map.containsKey(mask)) ? Math.max(map.get(mask), len) : len;
        map.put(mask, longer);
    }
    for(int key1 : map.keySet())
        for(int key2 : map.keySet())
            if((key1 & key2) == 0)
                res = Math.max(res, map.get(key1)*map.get(key2));
    return res;
}
```

The solution 1 is not fast. So there must be some place can be optimized. 

Based on the time complexity O(n<sup>2</sup> * w), we can optimaze n<sup>2</sup> or `w`.

From n<sup>2</sup> to `n * log(n)`, can sort the `words` reduce time complexity? 

If we check two words from longer length to short length, when there is no possible to get a larger product than the existing product, we can break the loop. This may reduce the average time complexity, but it will be still O(n<sup>2</sup> * w) in corner case (only short words have no shared common letters).

So can we reduce `w` to `1`? 

Yep, we can! To check if two words share common letters, we don't need to worry about the duplicated letters of a word. We just need to know if a letter appear or not in the word.

Because each word will contain only lower case letters, we can use an integer to represent all appeared letters of a word. There are at most 26 letters in a word, integer has 32 bit. we can use differt bit of an integer to represent the letter in a word.

When we have the integers which use bit to represent the words, we can use bit AND operation to check if two integers have `1` in the same location, in the problem it means if two words have common letters.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the input `words`. 
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `words`