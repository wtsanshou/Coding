# 628. Maximum Product of Three Numbers

### LeetCode

## Question

Given an integer array, find three numbers whose product is maximum and output the maximum product.

**Example 1:**
```
Input: [1,2,3]
Output: 6
```

**Example 2:**
```
Input: [1,2,3,4]
Output: 24
```

**Note:**

1.  The length of the given array will be in range [3,10<sup>4</sup>] and all elements are in the range [-1000, 1000].
2.  Multiplication of any three numbers in the input won't exceed the range of 32-bit signed integer.

## Solutions

* Java1
```
public int maximumProduct(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length-1;
        int m1 = nums[n-2]*nums[n-1]*nums[n];
        int m2 = nums[0]*nums[1]*nums[n];
        return Math.max(m1, m2);
    }
```

## Explanation

* **worst-case time complexity:** O(n*log(n))
* **worst-case space complexity:** O(n)