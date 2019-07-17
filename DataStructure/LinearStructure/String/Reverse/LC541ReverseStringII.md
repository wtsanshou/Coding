# LC541. Reverse String II

### LeetCode

## Question

Given a string and an integer k, you need to reverse the first k characters for every 2k characters counting from the start of the string. If there are less than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and left the other as original.

**Example:**
```
Input: s = "abcdefg", k = 2
Output: "bacdfeg"
```

**Restrictions:**

1.	The string consists of lower English letters only.
2.	Length of the given string and k will be in the range [1, 10000]

## Solutions

### Solution 1

* C++
```
class Solution {
public:
    void reverseStrFromTo(string& s, int i, int j)
    {
        while(i < j)
            swap(s[i++], s[j--]);
    }
    string reverseStr(string s, int k) {
        int n = s.length();
        for(int i=0; i<n; i+=2*k)
        {
            int j = i+k-1;
            while(j>=n) j--;
            reverseStrFromTo(s, i, j);
        }
        return s;
    }
};
```

This is not a difficult question. But you need to clear what is the requirement.

1. Reverse the first k characters for every 2k characters.
2. If there are less than k characters left, reverse all of them.
3. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters only.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(1)`.
