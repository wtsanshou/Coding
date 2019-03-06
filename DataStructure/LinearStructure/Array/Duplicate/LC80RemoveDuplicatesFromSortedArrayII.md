# LC80. Remove Duplicates from Sorted Array II

### LeetCode

## Question

Follow up for "Remove Duplicates":

What if duplicates are allowed at most twice?

**For example**
```
Given sorted array nums = [1,1,1,2,2,3],
Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.
```

## Solutions

### Solution 1

* C++
```
int removeDuplicates(vector<int>& nums) {
    int n = nums.size();
    int i=0;
    for(int j=0; j<n; ++i, ++j)
    {
        if(i==0) continue;
        while(nums[j]==nums[j-1] &&(j+1<n && nums[j]==nums[j+1])) j++;
        nums[i] = nums[j];
    }
    return i;
}
```

Using two pointers `i` and `j`. `i` for writing legal numbers, `j` for finding legal numbers (not equals both left and right).

* **worst-case time complexity:** `O(N)`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(1)`

### Solution 2

* C++
```
int removeDuplicates(vector<int>& nums) {
    int i = 0;
    for (int n : nums)
        if (i < 2 || n > nums[i-2])
            nums[i++] = n;
    return i;
}
```

Similar idea, but because the `nums` is sorted, so the legal numbers `n` just should be larger than `nums[i-2`. 

* **worst-case time complexity:** `O(N)`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(1)`
