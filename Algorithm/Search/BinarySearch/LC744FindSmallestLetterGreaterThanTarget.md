# LC744. Find Smallest Letter Greater Than Target

### LeetCode

## Question

Given a list of sorted characters letters containing only lowercase letters, and given a target letter target, find the smallest element in the list that is larger than the given target.

Letters also wrap around. For example, if the target is target = 'z' and letters = ['a', 'b'], the answer is 'a'.

Examples:

```
Input:
letters = ["c", "f", "j"]
target = "a"
Output: "c"
```

```
Input:
letters = ["c", "f", "j"]
target = "c"
Output: "f"
```

```
Input:
letters = ["c", "f", "j"]
target = "d"
Output: "f"
```

```
Input:
letters = ["c", "f", "j"]
target = "g"
Output: "j"
```

```
Input:
letters = ["c", "f", "j"]
target = "j"
Output: "c"
```

```
Input:
letters = ["c", "f", "j"]
target = "k"
Output: "c"
```

**Note:**

* letters has a length in range [2, 10000].
* letters consists of lowercase letters, and contains at least 2 unique letters.
* target is a lowercase letter.

## Solutions

* C#1
```
public char NextGreatestLetter(char[] letters, char target) {
    int n = letters.Length;
    if(target >= letters[n-1]) return letters[0];
    int i=0, j=n-1;
    while(i < j){
        int mid = i + (j-i)/2;
        if(target < letters[mid]) j = mid;
        else i = mid + 1;
    }
    return letters[i];
}
```

## Explanation

Classic binary search.

A corner case: if the target equals or larger than the last letter of the array, the result is the first letter of the array.

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)
