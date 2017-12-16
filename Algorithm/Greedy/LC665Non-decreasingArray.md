# LC665. Non-decreasing Array

### LeetCode

## Question

Given an array with n integers, your task is to check if it could become non-decreasing by modifying at most 1 element.

We define an array is non-decreasing if array[i] <= array[i + 1] holds for every i (1 <= i < n).

**Example 1:**

```
Input: [4,2,3]
Output: True
```

**Explanation:**

You could modify the first 4 to 1 to get a non-decreasing array.

**Example 2:**

```
Input: [4,2,1]
Output: False
```

**Explanation:** 

You can't get a non-decreasing array by modify at most one element.

**Note:** 

The n belongs to [1, 10,000].

## Solutions

* C#1

```
public class Solution {
    public bool CheckPossibility(int[] nums) {
        for(int i=0; i<nums.Length-1; ++i){
            if(i+2<nums.Length && nums[i] > nums[i+1])
                return i==0 ? CheckFrom(nums[i], nums, i+2) || CheckFrom(nums[i+1], nums, i+2)
                            : (nums[i]>=nums[i-1] && CheckFrom(nums[i], nums, i+2)) || (nums[i+1]>=nums[i-1] && CheckFrom(nums[i+1], nums, i+2));
        }
        return true;
    }
    
    private bool CheckFrom(int first, int[] nums, int start){
        if(first > nums[start]) return false;
        for(int i=start; i<nums.Length-1; ++i){
            if(nums[i] > nums[i+1]) return false;
        }
        return true;
    }
}
```

## Explanation

When you meet a decreasing pair at the first time, imagine removing one of them, and see if the current number is not less than previous number and no larger than next number.

**Corner Cases:**

1. When check the first number, you don't need to compare it with previous number.
2. Don't forget to compare the current number with previous number. 

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)
