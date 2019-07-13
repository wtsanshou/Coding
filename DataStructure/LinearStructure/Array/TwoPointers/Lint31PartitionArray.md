# Lint31. Partition Array

### LintCode

## Question

Given an array nums of integers and an int k, partition the array (i.e move the elements in "nums") such that:

* All elements < k are moved to the left
* All elements >= k are moved to the right

Return the partitioning index, i.e the first index i nums[i] >= k.

You should do really partition in array nums instead of just counting the numbers of integers smaller than k.

If all elements in nums are smaller than k, then return nums.length


**Example 1:**
```
Input:
[],9
Output:
0
```

**Example 2:**
```
Input:
[3,2,2,1],2
Output:1
Explanation:
the real array is[1,2,2,3].So return 1
```

**Follow up**

* Can you partition the array in-place and in O(n)?

## Solutions

### Solution 1

* Java
```
public int partitionArray(int[] nums, int k) {
    int i=0, j=nums.length-1;
    int max = Integer.MIN_VALUE;
    for(int n : nums)
        max = Math.max(max, n);
    while(i<j){
        while(i<j && nums[i]<k) i++;
        while(i<j && nums[j]>=k) j--;
        
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    return (k>max && i>0) ? i+1 : i;
}
```

Using two pointers `i` and `j` starting from head and tail. Point `i` to the number which is less than `k` in the left, point `j` to the number which is equal or larger than `k` in the right. Swap the two number. Continue this process until `i>=j`.

**Corner Cases:** 

1. `nums` is empty
2. k is less than the minimum number in the `nums`.
3. k is larger than the maximum number in the `nums`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `input`.
* **worst-case space complexity:** `O(1)`.
