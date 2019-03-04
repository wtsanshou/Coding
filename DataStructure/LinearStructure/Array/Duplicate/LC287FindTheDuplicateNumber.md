# LC287. Find the Duplicate Number

### LeetCode

## Question

Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

Note:

1.  You must not modify the array (assume the array is read only).
2.  You must use only constant, O(1) extra space.
3.  Your runtime complexity should be less than O(n<sup>2</sup>).
4.  There is only one duplicate number in the array, but it could be repeated more than once.

## Solutions

### Solution 1

* C++ (16ms) 
```
int findDuplicate(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    for(int i=1; i<nums.size(); ++i)
        if(nums[i]==nums[i-1]) return nums[i];
    return -1;
}
```

Sort the array `nums`, the duplicated number must be adjacent.

* **worst-case time complexity:** `O(N*log(N))`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(log(N))`, where `N` is the size of the input `nums`.

### Solution 2

* C++ (24ms)
```
int findDuplicate(vector<int>& nums) {
    if(nums.size()>1)
    {
        int i=1, j=nums.size()-1, mid, count;
        while(i<j)
        {
            mid = i+(j-i)/2;
            count=0;
            for(int n : nums)
            {
                if(n<=mid) count++;
            }
            //the numsbers smaller than mid are less, it means the duplicate number must be larger than mid
            if(count <= mid) i = mid+1; 
            else j = mid;
        }
        return i;
    }
    return -1;
}
```

1. The number of `num` who less than the location `mid` <= `mid`: there is no duplicated number in the range `[1, mid]`, the duplicated number must be in the range `[mid+1, n]`
2. The number of `num` who less than the location `mid` > `mid`: there is duplicated number in the range `[1, mid]`

* **worst-case time complexity:** `O(N*log(N))`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(1)`

### Solution 3

* Java (0ms)
```
public int findDuplicate(int[] nums) {
    int n = nums.length;
    for(int num : nums){
        int id = (num-1+n) % n;
        if(nums[id] < 0) return id+1;
        nums[id] -= n;
    }
    return -1;
}
```

The idea is from <a href="LC448FindAllNumbersDisappearedInAnArray.md">LC448. Find All Numbers Disappeared in an Array</a>. Trate the number as index of array, mark (minus `n`) the viewed index. If view a marked index, the duplicated number is the marked index.

* **worst-case time complexity:** `O(N)`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(1)`




