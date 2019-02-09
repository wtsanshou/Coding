# LC26. Remove Duplicates from Sorted Array

### LeetCode

## Question

Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

**For example**

```
Given input array nums = [1,1,2],
Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.
```

## Solutions

* C++1 (29ms) O(n)
```
int removeDuplicates(vector<int>& nums) {
    int i= !nums.empty();
    for(int j=1; j<nums.size(); ++j)
    {
        if(nums[i-1] < nums[j]) 
            nums[i++] = nums[j];
    }
    return i;
}
```

* C++2 (32ms) O(n)
```
int removeDuplicates(vector<int>& nums) {
    int len = nums.size();
    if(len<2) return len;
    int i=1;
    for(int j=1;j<len; j++)
    {
        while(nums[i-1]==nums[j] && j<len) j++;
        if(i==j)
        {
            i++;
            continue;
        }
        if(j<len)
        {
            nums[i++] = nums[j];
        }
    }
    return i;
}
```

* C++3 (40ms) O(n)
```
int removeDuplicates(vector<int>& nums) {
    int i = !nums.empty();
    for (int n : nums)
        if (n > nums[i-1])
            nums[i++] = n;
    return i;
}
```

* Java1 (2ms)
```
public int removeDuplicates(int[] nums) {
    int i=1, j=1, n=nums.length;
    while(j<n)
    {
        if(nums[j]==nums[j-1]) 
        {
            j++;
            continue;
        }
        nums[i++] = nums[j++];
    }
    return i;
}
```

* Java2 (1ms)
```
public int removeDuplicates(int[] nums) {
    int i=1, n=nums.length;
    for(int j=1; j<n; ++j)
    {
        if(nums[j]!=nums[j-1]) nums[i++] = nums[j];
    }
    return i;
}
```

## Explanation

Using two pointers, one for finding the unique number, one for writing the unique number

* **worst-case time complexity:** O(N), where `N` is the length of the input `nums`.
* **worst-case space complexity:** O(1).
