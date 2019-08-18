# Lint402. Continuous Subarray Sum

### LintCode (Medium)

## Question

Given an integer array, find a continuous subarray where the sum of numbers is the biggest. Your code should return the index of the first number and the index of the last number. (If their are duplicate answer, return the minimum one in lexicographical order)

**Example 1:**
```
Input: 
[-3, 1, 3, -3, 4]

Output: 
[1, 4]
```

**Example 2:**
```
Input: 
[0, 1, 0, 1]

Output: 
[0, 3]

Explanation: 
The minimum one in lexicographical order.
```

## Solutions

## Solution 1

* Java
```
public List<Integer> continuousSubarraySum(int[] A) {
    int n = A.length;
    List<Integer> res = new ArrayList<>();
    res.add(0);
    res.add(0);
    long maxVal = Long.MIN_VALUE;
    
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j <= n; j++) {
            int sum = 0;
            for (int k = i; k <j; k++)
                sum += A[k];
            if (sum > maxVal) {
                res.set(0, i);
                res.set(1, j - 1);
                maxVal = sum;
            }
        }
    }
    
    return res;
}
```

Search all possible ranges, get the sum of this range, record indexes of the maximum sum range.

**Complexity:**

* **worst-case time complexity:** O(n<sup>3</sup>), where `n` is the number of `A`.
* **worst-case space complexity:**  `O(1)`.

### Solution 2

* Java
```
private int[] continuousSubarraySum(int[] A) {
    int n = A.length;
    long[] prifixSum = new long[n + 1];
    List<Integer> res = new ArrayList<>();
    res.add(0);
    res.add(0);
    long maxVal = Long.MIN_VALUE;
    
    for (int i = 1; i <= n; i++) {
        prifixSum[i] = prifixSum[i - 1] + A[i - 1];
    }
    
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j <= n; j++) {
            if (prifixSum[j] - prifixSum[i] > maxVal) {
                res.set(0, i);
                res.set(1, j - 1);
                maxVal = prifixSum[j] - prifixSum[i];
            }
        }
    }
    
    return res;
}
```

Using prefix sum could pre-calculate the sum of range, so that reduce one loop in the **Solution 1**.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the number of `A`.
* **worst-case space complexity:**  `O(n)`, where `n` is the number of `A`.


### Solution 3

* Java
```
public List<Integer> continuousSubarraySum(int[] A) {
    List<Integer> res = new ArrayList<>();
    res.add(0);
    res.add(0);
    long maxVal = Long.MIN_VALUE;
    long preSum = 0;
    int start = 0;
    int end = 0;
    
    for (int i = 0; i < A.length; i++) {
        if (preSum + A[i] < A[i]) {
            preSum = A[i];
            start = i;
            end = i;
        } else {
            preSum += A[i];
            end = i;
        }
        
        if (maxVal < preSum) {
            res.set(0, start);
            res.set(1, end);
            maxVal = preSum;
        }
    }
    
    return res;
}
```

The key of this solution is that when a prefix sum plus `A[i]` is less than `A[i]`, a single `A[i]` is bigger than the whole prefix sum `preSum`. There is no need to continue the `preSum`. We can start a new `preSum` starting from `A[i]` ending from `i` as well.

**Complexity:**

* **worst-case time complexity:** O(n), where `n` is the number of `A`.
* **worst-case space complexity:**  `O(1)`.


