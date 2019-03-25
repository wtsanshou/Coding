# LC283. Move Zeroes

### LeetCode

## Question

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

Note:

1.	You must do this in-place without making a copy of the array.
2.	Minimize the total number of operations.

## Solutions

### Solution 1

* C++1
```
void moveZeroes(vector<int>& nums) {
    for(int j=0, i=0; j<nums.size(); ++j)
    {
        if(nums[j]!=0)
        {
            if(i!=j)
            {
                nums[i] = nums[j];
                nums[j] = 0;
            }
            i++;
        }
    }
}
```

* Java
```
public void moveZeroes(int[] nums) {
    int slow=0, fast=0, n=nums.length;
    while(fast<n)
    {
        while(fast<n-1 && nums[fast]==0) fast++;
        if(slow==fast)
        {
            slow++;
            fast++;
            continue;
        }
        nums[slow++] = nums[fast];
        nums[fast++] = 0;
    }
}
```

Using two pointers `slow` ans `fast`. `fast` is to find the non-zero elements, `slow` is to wirte the non-zero elements.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(1)`
