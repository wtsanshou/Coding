# LC75. Sort Colors

### LeetCode

## Question

Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note:

You are not suppose to use the library's sort function for this problem.

Follow up:

* A rather straight forward solution is a two-pass algorithm using counting sort.
* First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.
* Could you come up with an one-pass algorithm using only constant space?

## Solutions

### Solution 1

* Java (0 ms, 37.4 MB)
```
class Solution {
    public void sortColors(int[] nums) {
        int i=0;
        for(int j=0; j<nums.length; j++)
            if(nums[j]==0)
                swap(nums, i++, j);
            
        for(int j=i; j<nums.length; j++)
            if(nums[j] == 1)
                swap(nums, i++, j);
    }
        
    private void swap(int[] nums, int i, int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

1. swap `0` to left
2. swap `1` to the middle.

* **worst-case time complexity:** `O(N)`, where `N` is the length of the `nums`.
* **worst-case space complexity:** `O(1)`.

### Solution 2

* C++
```
void sortColors(vector<int>& nums) {
    for(int i=0, j=0, k=0; k<nums.size(); ++k)
    {
        int tem = nums[k];
        nums[k] = 2;
        if(tem < 2) nums[j++] = 1;
        if(tem == 0) nums[i++] = 0;
    }
}
```

Using 3 pointers to record the color:

```
i -> 0 (only cover 0, size is the number of 0)
j -> 1 (only cover 0 and 1, size is the number of 0 and 1)
k -> 2 (cover 0, 1, and 2, size is the whole nums)
```

* **worst-case time complexity:** `O(N)`, where `N` is the length of the `nums`.
* **worst-case space complexity:** `O(1)`.
