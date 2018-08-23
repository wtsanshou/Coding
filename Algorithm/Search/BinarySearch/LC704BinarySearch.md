# LC704. Binary Search

### LeetCode

## Question

Given a sorted (in ascending order) integer array nums of n elements and a target value, write a function to search target in nums. If target exists, then return its index, otherwise return -1.


**Example 1:**
```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

**Example 2:**
```
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

**Note:**

* You may assume that all elements in nums are unique.
* n will be in the range [1, 10000].
* The value of each element in nums will be in the range [-9999, 9999].

## Solutions

* Scala1
```
object Solution {
    def search(nums: Array[Int], target: Int): Int = {
        search(nums, target, 0, nums.length)
    }
    
    def search(nums: Array[Int], target: Int, left: Int, right: Int): Int = {
        if(left >= right) return -1
        val mid = left + (right - left) / 2
        if(target == nums(mid)) return mid
        if(target < nums(mid)) search(nums, target, left, mid) else search(nums, target, mid+1, right)
    }
}
```

## Explanation

Classic binary search.

* **worst-case time complexity:** O(log(n)), where `n` is the length of the array `nums`.
* **worst-case space complexity:** O(log(n)), where `n` is the length of the array `nums`.
