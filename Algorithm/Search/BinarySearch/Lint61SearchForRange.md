# Lint61. Search for a Range

### LintCode

## Question

Given a sorted array of n integers, find the starting and ending position of a given target value.

If the target is not found in the array, return [-1, -1].

**Example 1:**

```
Input:
[]
9

Output:
[-1,-1]
```

**Example 2:**

```
Input:
[5, 7, 7, 8, 8, 10]
8
Output:
[3, 4]
```

**Challenge**

* O(log n) time.

## Solutions

### Solution 1

* Java
```
public int[] searchRange(int[] A, int target) {
    int lastIndex = A.length - 1;
    int i = 0, j = lastIndex;
    int targetId = -1;
    while (i <= j) {
        int mid = i + (j - i) / 2;
        if (A[mid] == target) {
            targetId = mid;
            break;
        } else if (A[mid] < target) {
            i = mid + 1;
        } else {
            j = mid - 1;
        }
    }
    
    if (targetId == -1) return new int[] {-1, -1};
    
    int[] res = new int[] {0, lastIndex};
    for (i = targetId; i > 0 && A[i] == target; i--) { // could use another binary search
        if (A[i] != A[i - 1])
            res[0] = i;
    }
    
    for (j = targetId; j < lastIndex && A[j] == target; j++) { // could use another binary search
        if (A[j] != A[j + 1])
            res[1] = j;
    }
    
    return res;
} 
```

It's easy to find the target using binary search, but be carefull the corner case. Must be carefull `i < j` or `i <= j`.

**Corner test case :**

```
Input:
[1]
1

Output:
[0,0]
```

After find the index of the target, we have to seach the range of the target starting from the found target index to its both side. Be careful the edge case (targets include first element and/or the last element), so I set the initial result as `new int[] {0, lastIndex}`.

It's `O(n)` time complexity, because the test case could be that all elements are the target.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `A`.
* **worst-case space complexity:** `O(1)`.

