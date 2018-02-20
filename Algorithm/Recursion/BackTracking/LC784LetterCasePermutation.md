# LC784. Letter Case Permutation

### LeetCode

## Question

Given a string S, we can transform every letter individually to be lowercase or uppercase to create another string.  Return a list of all possible strings we could create.

**Examples:**

```
Input: S = "a1b2"
Output: ["a1b2", "a1B2", "A1b2", "A1B2"]
```

```
Input: S = "3z4"
Output: ["3z4", "3Z4"]
```

```
Input: S = "12345"
Output: ["12345"]
```

**Note:**

* S will be a string with length at most 12.
* S will consist only of letters or digits.

## Solutions

* Java1
```
class Solution {
    public List<String> letterCasePermutation(String S) {
        List<String> res = new ArrayList<>();
        addCases(res, "", 0, S);
        return res;
    }
    
    private void addCases(List<String> res, String cases, int start, String S){
        for(int i=start; i<S.length(); ++i){
            char target = S.charAt(i);
            if(Character.isLetter(target))
                addCases(res, cases+Character.toUpperCase(target), i+1, S);
            cases += Character.toLowerCase(target);
        }
        res.add(cases);
    }
}
```

## Explanation

Imagine a binary tree, when meet a letter, go two way. One case uses lower letter, another use upper letter.

* **worst-case time complexity:** O(2<sup>n</sup>), where n is the length of S.
* **worst-case space complexity:** O(2<sup>n</sup>), where n is the length of S.
