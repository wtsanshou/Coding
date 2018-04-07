# LC27. Remove Element

### LeetCode

## Question

Given an array and a value, remove all instances of that value in place and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example:**
```
Given input array nums = [3,2,2,3], val = 3
Your function should return length = 2, with the first two elements of nums being 2.
```

## Solutions

* C++1 
```
int removeElement(vector<int>& nums, int val) {
    int i=0;
    for(int j=0; j<nums.size(); ++j)
    {
        if(nums[j] != val)
            nums[i++] = nums[j];
    }
    return i;
}
```

* C++2
```
int removeElement(vector<int>& nums, int val) {
    nums.erase(remove(nums.begin(), nums.end(), val),nums.end());
    return nums.size();
}
```

* Java1 
```
public int removeElement(int[] nums, int val) {
    int i=0;
    for(int j=0; j<nums.length; ++j)
    {
        if(nums[j]!=val)
        {
            if(i!=j) nums[i++]=nums[j];
            else i++;
        }
    }
    return i;
}
```

* Java2
```
public int removeElement(int[] nums, int val) {
    int len = A.length;
    for (int i = 0 ; i< len; ++i){
        while (A[i]==elem && i< len) {
            A[i]=A[--len];
        }
    }
    return len;
}
```

## Explanation

Using two pointers `i` and `j`, `j` is to traverse the array, move `i` only when the element does not equal `val`.

* **worst-case time complexity:** `O(N)`, where `N` is the length of the `nums`.
* **worst-case space complexity:** `O(1)`.
