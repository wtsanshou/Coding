# LC424. Longest Repeating Character Replacement

### LeetCode

## Question

Given a string that consists of only uppercase English letters, you can replace any letter in the string with another letter at most k times. Find the length of a longest substring containing all repeating letters you can get after performing the above operations.

**Note:**

* Both the string's length and k will not exceed 10<sup>4</sup>.

**Example 1:**

```
Input:
s = "ABAB", k = 2

Output:
4

Explanation:
Replace the two 'A's with two 'B's or vice versa.
```

**Example 2:**

```
Input:
s = "AABABBA", k = 1

Output:
4

Explanation:
Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
```

## Solutions

### Solution 1

* Java
```
public int characterReplacement(String s, int k) {
    int[] count = new int[128];
    int start=0, maxCount=0, maxLen=0;
    char[] sc = s.toCharArray();
    for(int end=0; end<sc.length; end++){
        maxCount = Math.max(maxCount, ++count[sc[end]]); //the longest repeating letter from start to end
        while(end-start+1 - maxCount > k) //Always try to check a window which is larger or equal than the existing maxLen. When replacing k letters cannot make the substring from start to end to be all the same letter. 
            count[sc[start++]]--; //move the start point of the window to right
       
        maxLen = Math.max(maxLen, end-start+1); //A window ([start, end]) can perform the replacement operation.
    }
    return maxLen;             
}
```

Set a window (`[start, end]`), check if eplacing k letters can make the substring from start to end to be all the same letter.

`end-start+1 - maxCount > k`: using the length of the window minus the number of the longest repeating letter in the window, we can know how many (`k`?) letters we need to replace to make the whole window to be the same letter.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(1)`.

## Solution 2

* C++ (9ms)
```
int characterReplacement(string s, int k) {
    int n=s.size(), start=0, max_same=0;
    int letter[128] = {0};
    for(int i=0; i<n; ++i)
        if((max_same = max(max_same, ++letter[s[i]])) < i-start+1-k) 
            --letter[s[start++]];
    return n - start;
}
```

`max_same = max(max_same, ++letter[s[i]])) < i-start+1-k` is the same as `i-start+1 - max_same > k`. 

Here we don't need `maxLen = Math.max(maxLen, end-start+1)`, because we always try to check a window which is larger or equal than the existing maxLen. So the `n - start` will always larger or equal than the existing maxLen.

So `n - start` is always the result no matter if the substring `[start, n)` can (`n-start >= maxLen`) perform the replacement operation or not (`n-start = maxLen`).

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(1)`.
