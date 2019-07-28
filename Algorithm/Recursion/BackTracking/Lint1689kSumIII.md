# Lint1689. k Sum III

### LintCode

## Question

Given n positive integers, integer k and a number target.

Find k odd numbers or k even numbers where sum is target. Calculate how many solutions there are?

**Example 1:**

```
Given 
[1,2,3,4], k = 2,target = 4

Input:
[1,2,3,4]
4
1

Output:
1

Explanation:
There are one solutions: [1,3].
```

**Example 2:**

```
Given 
[9,1,4,4], k = 3,target = 46

Input:
[9,1,4,4]
3
46

Output:
0
```

**Notice**

* 1≤ n ≤ 20
* k ≤ n
* There may be duplicate numbers in n numbers
* For the two solutions whose values correspond to the same, as long as there are different indexes, they can be regarded as two different solutions.

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param a: the array a
     * @param k: the integer k
     * @param target: the integer target
     * @return: return the number of legal schemes
     */
    public int getAns(int[] a, int k, int target) {
        return getKSum(a, k, target, true, 0, 0) + getKSum(a, k, target, false, 0, 0);
    }
    
    private int getKSum(int[] a, int k, int target, boolean even, int count, int start) {
        if (start >= a.length) {
            if (target == 0 && count == k)
                return 1;
            return 0;
        }
        if (target == 0  && count == k) 
            return 1;

        if (count > k) 
            return 0;
        
        int res = 0;
        for (int i = start; i < a.length; i++) {
            if (a[i] % 2 == 0) {
                if (even == true)
                    res += getKSum(a, k, target - a[i], true, count + 1, i + 1);
            }
            else {
                if (even == false)
                    res += getKSum(a, k, target - a[i], false, count + 1, i + 1);
            }
        }
        return res;
    }
}
```

* Java (refactor)
```
public class Solution {
    /**
     * @param a: the array a
     * @param k: the integer k
     * @param target: the integer target
     * @return: return the number of legal schemes
     */
    public int getAns(int[] a, int k, int target) {
        return getKSum(a, k, target, true, 0, 0) + getKSum(a, k, target, false, 0, 0);
    }
    
    private int getKSum(int[] a, int k, int target, boolean even, int count, int start) {
        if (start >= a.length) {
            if (target == 0 && count == k)
                return 1;
            return 0;
        }
        if (target == 0  && count == k) 
            return 1;
            
        if (count > k) 
            return 0;
        
        int res = 0;
        for (int i = start; i < a.length; i++) {
            if (a[i] % 2 == 0 && even == true)
                    res += getKSum(a, k, target - a[i], true, count + 1, i + 1);
            
            if (a[i] % 2 != 0 && even == false)
                    res += getKSum(a, k, target - a[i], false, count + 1, i + 1);
        }
        return res;
    }
}
```

Quite similar with <a href="Lint90kSumII.md">Lint90. k Sum II</a>. Here just need to `Find k odd numbers or k even numbers where sum is target`, and do not need to worry about duplicated solutions. So we don't need to sort the input `a`. Instead of keep all found numbers in a list, we can use `target - a[i]` and a boolean mark `even` to indicate the sum of our found numbers and the `odd_or_even` of our found numbers. Finally, we just need to check how many `even solutions` and how many `odd solutions` in total.

**Exit point:**

1. `start >= a.length`, no further solutions could be found, but must check if the found numbers is a solution.
2. `target == 0  && count == k`, found a solution.
3. `count > k`, no further solutions could be found.


**Complexity:**

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the length of the input `a`.
* **worst-case space complexity:** O(n), where `n` is the length of the input `a`.

## Follow up

1. What if asking for listing all solutions?
2. What if asking for solutions without duplicates?


