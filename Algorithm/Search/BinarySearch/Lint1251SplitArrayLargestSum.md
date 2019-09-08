# Lint1251. Split Array Largest Sum

### LintCode (Hard)

## Quesiton

Given an array which consists of non-negative integers and an integer m, we are going to split the array into m non-empty continuous subarrays. Write an algorithm to minimize the largest sum among these m subarrays.

**Example 1:**
```
Input：
[7,2,5,10,8], m = 2

Output：
18

Explanation：
    There are four ways to split nums into two subarrays.
    The best way is to split it into [7,2,5] and [10,8],
    where the largest sum among the two subarrays is only 18.
```

**Example 2:**
```
Input：
[1,4,4], m = 3

Output：
4

Explanation：
    There is a way to split nums into three subarrays.
    The best way is to split it into [1], [4] and [4],
    where the largest sum among the three subarrays is only 4.
```

**Notice**

If n is the length of array, assume the following constraints are satisfied:

* 1 ≤ n ≤ 1000
* 1 ≤ m ≤ min(50, n)

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param nums: a list of integers
     * @param m: an integer
     * @return: return a integer
     */
    public int splitArray(int[] nums, int m) {
        int max = 0;
        long sum = 0;
        for (int num : nums) {
            max = Math.max(max, num);
            sum += num;
        }
        
        if (m == 1) {
            return (int)sum;
        }
        
        long left = max, right = sum;
        while (left <= right) {
            long mid = left + (right - left) / 2;
            
            if (isValid(nums, m, mid)) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        
        return (int)left;
    }
    
    private boolean isValid(int[] nums, int m, long target) {
        int count = 1;
        long total = 0;
        
        for (int num : nums) {
            total += num;
            if (total > target) {
                total = num;
                count++;
            }
            
            if (count > m) {
                return false;
            }
        }
        
        return true;
    }
}
```

The target result must between `max` and `sum`. Using binary search int the range [`max`, `sum`] to find the final result. Similar as the question <a href="Lint183WoodCut.md">Lint183. Wood Cut</a>

**Complexity:**

* **worst-case time complexity:** `O(n * log(sum))`, where `n` is the length of the `nums`, `sum` is the sum value of `nums`.
* **worst-case space complexity:**  `O(1)`.
