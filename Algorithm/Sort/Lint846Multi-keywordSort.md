# Lint846. Multi-keyword Sort

Given n students and their test scores, expressed as (student number, test scores), sort by test scores in descending order, if the test scores are the same, sort the student number in ascending order.

**Example1**
```
Input: array = [[2,50],[1,50],[3,100]]
Output: [[3,100],[1,50],[2,50]]
```

**Example2**
```
Input: array = [[2,50],[1,50],[3,50]]
Output: [[1,50],[2,50],[3,50]]
```

## Solutions

### Solution 1

* Java
```
public int[][] multiSort(int[][] array) {
    Arrays.sort(array, (a, b) -> {
        if(a[1] == b[1])
            return Integer.compare(a[0], b[0]);
        else
            return Integer.compare(b[1], a[1]);
    });
    return array;
}
```

**Complexity:**

* **worst-case time complexity:** `O(n * log(n))`, where `n` is the length of the `array`.
* **worst-case space complexity:** `O(log(n))`, where `n` is the length of the `array`.
