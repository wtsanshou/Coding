# Lint31. Partition Array

### LintCode

## Question

Given an array nums of integers and an int k, partition the array (i.e move the elements in "nums") such that:

* All elements < k are moved to the left
* All elements >= k are moved to the right
* Return the partitioning index, i.e the first index i nums[i] >= k.

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

Output:
1

Explanation:

the real array is[1,2,2,3].So return 1
```

**Challenge** 

* Can you partition the array in-place and in O(n)?

**Notice**

You should do really partition in array nums instead of just counting the numbers of integers 

## Solutions

### Solution 1

* Java (208 ms)
```
public int partitionArray(int[] nums, int k) {
    Arrays.sort(nums);
 
    int i = 0;
    for (; i<nums.length; i++) {
        if (nums[i] >= k)
            return i;
    }
    
    return i;
}
```

The most straight forward way is to sort the `nums` first. Then just need to check the location of the number who is larger than or equals to `k`;

**Corner Cases:**

1. `k` is less than the minmum number in `nums`.
2. `k` is larger than the maximum number in `nums`.

**Complexity:**

* **worst-case time complexity:** `O(n * log(n))`, where `n` is the length of `nums`.
* **worst-case space complexity:** `O(log(n))`, where `n` is the length of `nums`.

### Solution 2

* Java (252 ms)
```
public int partitionArray(int[] nums, int k) {
    for (int i = 0, j = nums.length-1; i < j; i++, j--) {
        while (i < j && nums[i] < k) i++;
        while (i < j && nums[j] >= k) j--;
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
    int res = 0;
    for (; res < nums.length; res++) {
        if (nums[res] >= k)
            return res;
    }
    
    return res;
}
```

The question does not need the `nums` to be sorted after the patition. So, we do not actually need to sort all numbers in `nums`. 

So there is an `O(n)` solution. We just need to use two points `i` and `j` to search from left and right sides of `nums`. Let `i` points to a number who is larger than or equals to `k`; let 'j' points to a number who is less than `k`; Then swap `nums[i]` and `nums[j]`.

After change all the order in `nums`, we can serach the first index `i` where `nums[i] >= k`. 

**Strange Found**

From the sumbit result, the speed is slower than the `sort` **solution 1**. I don't think the test cases are enough to test the time complexity.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `nums`.
* **worst-case space complexity:** `O(1)`.
