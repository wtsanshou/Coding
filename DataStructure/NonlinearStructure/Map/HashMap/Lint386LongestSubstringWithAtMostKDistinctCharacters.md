# Lint386. Longest Substring with At Most K Distinct Characters

### LintCode

## Question

Given a string S, find the length of the longest substring T that contains at most k distinct characters.

**Example 1:**
```
Input: S = "eceba" and k = 3
Output: 4

Explanation: T = "eceb"
```

**Example 2:**
```
Input: S = "WORLD" and k = 4
Output: 4

Explanation: T = "WORL" or "ORLD"
```

## Solutions

### Solution 1

* Java
```
public int lengthOfLongestSubstringKDistinct(String s, int k) {
    char[] sArr = s.toCharArray();
    Map<Character, Integer> count = new HashMap<>();
    int start = 0, maxLen = 0;

    for(int i = 0; i < sArr.length; i++){
        if(!count.containsKey(sArr[i]))
            count.put(sArr[i], 0);
        count.put(sArr[i], count.get(sArr[i]) + 1);
        while(count.size() > k){
            count.put(sArr[start], count.get(sArr[start]) - 1);
            if(count.get(sArr[start]) <= 0)
                count.remove(sArr[start]);
            start++;
        }
        maxLen = Math.max(i - start + 1, maxLen);
    }
    return maxLen;
}
```

When I see the question, it's easy to come out a `Brute Force` solution: we can start from each character, can check all possible sub-string. But its time complexity is O(n<sup>2</sup>).

Can we do it faster? 

Yes, we can. We can keep a window slide which can expand to right and move out character from left. So we need a data structure to store the number of distinct characters in the window, also need to store the number of each character. HashMap is perfect for this requirements.

Then, we also need a pointer `start` to remember the index of the left edge of the window. We can expand to right one character each time. When the number of distinct characters in the window is more than `k`, move `start` pointer to right to reduce the size of the window. At the same time, update the HashMap `count`. When the number of distinct characters in the window is not more than `k`, we can check if the size of the window is the longest substring T that contains at most k distinct characters.

**Complexity:**

* **worst-case time complexity:** `O(n + k)`, where `n` is the length of the `s`, `k` is the number of most distinct characters limitation.
* **worst-case space complexity:** `O(n + k)`, where `n` is the length of the `s`, `k` is the number of most distinct characters limitation.
