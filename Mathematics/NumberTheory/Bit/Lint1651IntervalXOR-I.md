# Lint1651. Interval XOR I

### LintCode

## Question

Given an integer array A(index from 0 to n-1, where n is the size of this array), and an query list. Each query has two integers i and k. For each query, calculate the XOR of the numbers Ai, A(i + 1), ..., A(i+k-1).return the result list.

**Example1**
```
Input: A = [1,2,3,4] and query = [(0,2),(1,2)]

Output: [3,1]

Explanation:
1 ^ 2 = 3
2 ^ 3 = 1
```

**Example2**
```
Input: A = [1,2,4,8] and query = [(0,2),(2,2)]

Output: [3,12]

Explanation:
1 ^ 2 = 3
4 ^ 8 = 12
```

**Notice**

* You can use '^' to do it. In most languages '^' means XOR.
* In this problem k = 2 always.
* n <= 10000,number of queries <= 1000.
* Ai < 1000, i + k < n.

## Solutions

### Solution 1

* Java
```
public class Solution {
    public List<Integer> intervalXOR(int[] A, List<Interval> query) {
        List<Integer> res = new LinkedList<>();
        for (Interval q : query) {
            res.add(xor(A, q));
        }
        return res;
    }
    
    private int xor(int[] A, Interval query) {
        int res = 0;
        for (int i = query.start; i < query.start+query.end; i++)
            res ^= A[i];
        return res;
    }
}
```

`k = 2 always` is very confuse, not sure why. 

The question is very straight forward. Just do what the question asking.

**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the length of the input `query`, `m` is the length of `A`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `query`.
