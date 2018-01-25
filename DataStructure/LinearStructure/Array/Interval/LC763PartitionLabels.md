# LC763. Partition Labels

### LeetCode

## Question

A string S of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.

**Example 1:**
```
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
```

**Explanation:**

The partition is "ababcbaca", "defegde", "hijhklij".

This is a partition so that each letter appears in at most one part.

A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.

**Note:**

* S will have length in range [1, 500].
* S will consist of lowercase letters ('a' to 'z') only.

## Solutions

* Java1
```
public List<Integer> partitionLabels(String S) {
        int[] letters = new int[26];
        char[] schar = S.toCharArray();
        for(int i=0; i<S.length(); ++i)
            letters[schar[i] - 'a'] = i+1;
        int left=0, right=1;
        List<Integer> res = new ArrayList<>();
        for(int i=0; i<S.length(); ++i){
            int letter = schar[i] - 'a';
            if(letters[letter] > right)
                right = letters[letter];
            if(right == i+1){
                res.add(right-left);
                left = right;
                right += 1;
            }
        }
        return res;
    }
```

## Explanation

1. Record the most right location of each letter in the string `S`.
2. Start a interval from the first letter in the the string `S`.
3. In the interval, check if there is any letter which can extend the interval.
4. Only when `letters[letter]==right==i+1`, One interval is finished.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)