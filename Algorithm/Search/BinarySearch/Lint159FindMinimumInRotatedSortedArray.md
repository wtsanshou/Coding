# Lint159. Find Minimum in Rotated Sorted Array

### LintCode

## Question

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

**Example 1:**
```
Input：[4, 5, 6, 7, 0, 1, 2]

Output：0

Explanation：
The minimum value in an array is 0.
```

**Example 2:**
```
Input：[2,1]

Output：1

Explanation：
The minimum value in an array is 1.
```

**Notice**

* You can assume no duplicate exists in the array.

## Solutions

### Solution 1

* Java
```
public int findMin(int[] nums) {
    int i = 0, j = nums.length - 1;
    while (i < j) {
        int mid = i + (j - i) / 2;
        if (nums[i] < nums[j])
            break;
        else {
            if (nums[i] <= nums[mid]) 
                i = mid + 1;
            else
                j = mid;
        }
    }
    return nums[i];
}
```

Found a rule in Binary Search: 

1. If we need to return something in the `while` loop, we use **i <= j**.
2. If we do not need to return anything in the `while` loop, we use **i < j**.

There is a corner case for this question: all numbers in the search range `i` to `j` are sorted. In this case, `nums[i]` is the minimum value.

So we just need to specify this case first. Then, there are only two cases left:

1. `nums[i] <= nums[mid]`, we can sure the minimum value is in the right `[mid + 1, j]`
2. `nums[i] > nums[mid]`, we can also sure the minimum value is in the left `[i, mid]`

**Complexity:**

* **worst-case time complexity:** `O(log(n))`, where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(1)`.