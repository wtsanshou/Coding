# Lint183. Wood Cut

### LintCode (Hard)

## Question

Given n pieces of wood with length L[i] (integer array). Cut them into small pieces to guarantee you could have equal or more than k pieces with the same length. What is the longest length you can get from the n pieces of wood? Given L & k, return the maximum length of the small pieces.

**Example 1**
```
Input:
L = [232, 124, 456]
k = 7
Output: 114
Explanation: We can cut it into 7 pieces if any piece is 114cm long, however we can't cut it into 7 pieces if any piece is 115cm long.
```

**Example 2**
```
Input:
L = [1, 2, 3]
k = 7
Output: 0
Explanation: It is obvious we can't make it.
```

**Challenge**

* `O(n log(Len))`, where Len is the longest length of the wood.

**Notice**

* You couldn't cut wood into float length.
* If you couldn't get >= k pieces, return 0.

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param L: Given n pieces of wood with length L[i]
     * @param k: An integer
     * @return: The maximum length of the small pieces
     */
    public int woodCut(int[] L, int k) {
        int maxLen = 0;
        for (int len : L)
            maxLen = Math.max(maxLen, len);
            
        int i = 1, j = maxLen;
        
        while(i <= j) {
            int mid = i + (j - i) / 2;
            int count = count(L, mid);
            if (count < k)
                j = mid - 1;
            else
                i = mid + 1;
        }
        
        return j;
    }
    
    private int count(int[] L, int pieceLen) {
        int count = 0;
        for (int len : L)
            count += len / pieceLen;
        return count;
    }
}
```

The idea is to use binary search to try different length of pieces.

* If count pieces is less than `k`, it means the piece length `mid` is too long, so the result must be in the range `[i, mid - 1]`
* If count pieces is equals to or more than `k`, it means the piece length is possible, we can try longer piece in the range `[mid + 1, j]`.

**NOTE** `If you couldn't get >= k pieces, return 0.`, to implement this goal, we can use `j` to point the final result, we have to use `while(i <= j)`, so when `j` reach to length `1` and equals to `i`, and `mid=1`, it still process in and make `j = mid - 1`.

**Complexity:**

* **worst-case time complexity:** `O(n * log(m))`, where `n` is the length of the `L`, `m` is the maximum value in `L`.
* **worst-case space complexity:**  `O(1)`.

