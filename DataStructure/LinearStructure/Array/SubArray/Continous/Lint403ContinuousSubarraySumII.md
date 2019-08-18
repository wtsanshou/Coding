# Lint403. Continuous Subarray Sum II

### LintCode

## Quesiton

Given an circular integer array (the next element of the last element is the first element), find a continuous subarray in it, where the sum of numbers is the biggest. Your code should return the index of the first number and the index of the last number.

If duplicate answers exist, return any of them.

**Example 1:**
```
Input: [3, 1, -100, -3, 4]
Output: [4, 1]
```

**Example 2:**
```
Input: [1,-1]
Output: [0, 0]
```

**Challenge**

* O(n) time

## Solutions

### Solution 1

* Java
```
public class Solution {
    /*
     * @param A: An integer array
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    public List<Integer> continuousSubarraySumII(int[] A) {
        List<Integer> doubleList = new ArrayList<>();
        AddToList(doubleList, A);
        AddToList(doubleList, A);
        int n = A.length;
        
        return maxSubarraySum(doubleList);
    }
    
    private void AddToList(List<Integer> list, int[] A) {
        for (int a : A)
            list.add(a);
    }
    
    private List<Integer> maxSubarraySum(List<Integer> doubleList) {
        int n = doubleList.size();
        long[] prifixSum = new long[n + 1];
        List<Integer> res = new ArrayList<>(2);
        res.add(0);
        res.add(0);
        long maxVal = Long.MIN_VALUE;
        
        for (int i = 1; i <= n; i++) {
            prifixSum[i] = prifixSum[i - 1] + doubleList.get(i - 1);
        }
        
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j <= n && j < i + n / 2; j++) {
                if (prifixSum[j] - prifixSum[i] > maxVal) {
                    res.set(0, i);
                    res.set(1, (j - 1) % (n / 2));
                    maxVal = prifixSum[j] - prifixSum[i];
                }
            }
        }
        
        return res;
    }
}
```

For circular type of question, you can always think of double the input, so that we can generate a connection of head and tail in the middle of the doubleed input.

When we doubled the input `A`, it kind of become the question of <a href="LC523ContinuousSubarraySum.md">Lint402. Continuous Subarray Sum</a>. We can use the prefix sum solution to solve it.

**Corner Cases**

1. Cannot use the O(n) solution of <a href="LC523ContinuousSubarraySum.md">Lint402. Continuous Subarray Sum</a>. Because it cannot handle some corner cases. i.e `[16,-1,-2,-4,14,14,15]` which will make `start` point stay at `0`.
2. The disstance between `i` and `j` should not more than the length of the `input`. 

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the number of `A`.
* **worst-case space complexity:**  `O(n)`, where `n` is the number of `A`.

### Solution 2

* Java
```
public class Solution {
    /*
     * @param A: An integer array
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    public List<Integer> continuousSubarraySumII(int[] A) {
        List<Integer> max1 = continuousSubarraySum(A, Long.MIN_VALUE, (a, b) -> a < b);
          List<Integer> min2 = continuousSubarraySum(A, Long.MAX_VALUE, (a, b) -> a > b);

        long sum = sumOf(A);
        int n = A.length;
        
        return max1.get(2) > sum - min2.get(2) || sum == min2.get(2) ? 
                            max1.subList(0, 2) : 
                            Arrays.asList(((min2.get(1) + 1) % n), ((min2.get(0) - 1 + n) % n));
    }
    
    public List<Integer> continuousSubarraySum(int[] A, long val, BiPredicate<Long, Long> predict) {
        List<Integer> res = new ArrayList<>();
        res.add(0);
        res.add(0);
        res.add(0);
        long localval = 0;
        int start = 0;
        int end = 0;
        
        for (int i = 0; i < A.length; i++) {
            if (predict.test(localval + A[i], (long)A[i])) {
                localval = A[i];
                start = i;
                end = i;
            } else {
                localval += A[i];
                end = i;
            }
            
            if (predict.test(val, localval)) {
                res.set(0, start);
                res.set(1, end);
                res.set(2, (int)localval);
                val = localval;
            }
        }
        
        return res;
    }
}
```

To reach `O(n)`, we need to reverse thinking of the question. There are two type of maximum continuous subarray:

1. maximum continuous subarray in the middle of the input `A`.
2. maximum continuous subarray in the two sides of the input `A`.

Case 1 is just the question <a href="LC523ContinuousSubarraySum.md">Lint402. Continuous Subarray Sum</a>.

We can think the case 2 is also the question <a href="LC523ContinuousSubarraySum.md">Lint402. Continuous Subarray Sum</a>, but to find the minimum continuous subarray. The maximum continuous subarray is the opposite part of the result.

So, the idea is find the results of both scenarios, then the bigger one is the result.

**Corner Cases**

1. All input numbers are negative, in this case `sum == min2.get(2)`
2. To get the opposite part of the minimum continuous subarray, we can use `(min2.get(1) + 1) % n), ((min2.get(0) - 1 + n) % n)`, this will cover the edge cases.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of `A`.
* **worst-case space complexity:**  `O(1)`.
