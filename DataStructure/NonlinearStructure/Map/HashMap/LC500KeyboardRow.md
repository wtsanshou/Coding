# LC500. Keyboard Row

### LeetCode

## Question

Given a List of words, return the words that can be typed using letters of alphabet on only one row's of American keyboard like the image below.

**Example 1:**

```
Input: ["Hello", "Alaska", "Dad", "Peace"]
Output: ["Alaska", "Dad"]
```

**Note:**

1.	You may use one character in the keyboard more than once.
2.	You may assume the input string will only contain letters of alphabet.

## Solutions

### Solution 1

* C++ (3ms) O(mn)
```
vector<string> findWords(vector<string>& words) {
    char second[] = {'a', 's', 'd', 'f','g','h','j','k', 'l'};
    char third[] = {'z','x','c','v','b','n','m'};
    int count[128] = {0};
    for(char s : second)
        count[s]=count[toupper(s)] = 2;
    for(char t : third)
        count[t]=count[toupper(t)] = 3;
    vector<string> res;
    for(string word : words)
    {
        bool isInOneRow = true;
        for(int i=1; i<word.length(); ++i)
            if(count[word[i]]!= count[word[i-1]])
            {
                isInOneRow = false;
                break;
            }
        if(isInOneRow)
            res.push_back(word);
    }
    return res;
}
```

* Python
```
def findWords(self, words):
    keyboard = ["qwertyuiop", "asdfghjkl", "zxcvbnm"]
    keyMap = dict([(K,i) for i in range(3) for K in keyboard[i]])
    res =[]
    for word in words:
        isInOneRow = True
        W = word.lower()
        for j in range(1,len(W)):
            if (keyMap[W[j]] != keyMap[W[j-1]]):
                isInOneRow = False
                break
        if isInOneRow is True:
            res.append(word)
    return res
```

Using a `map` to map alphabets to their row number in American keyboard.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `words`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `words`.