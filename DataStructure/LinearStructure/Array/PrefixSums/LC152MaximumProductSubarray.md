# LC152. Maximum Product Subarray

### LeetCode

## Question

Find the contiguous subarray within an array (containing at least one number) which has the largest product.

**For example** 
```
given the array [2,3,-2,4],
the contiguous subarray [2,3] has the largest product = 6.
```

## Solutions

### Solution 1

* C++
```
int maxProduct(vector<int>& nums) {
    int left=1, right=1, res=INT_MIN, n=nums.size();
    for(int i=0; i<n; ++i)
    {
        left *= nums[i];
        right *= nums[n-i-1];
        res = max(res, max(left, right));
        left = (left==0) ? 1 : left;
        right = (right==0) ? 1 : right;
    }
    return res;
}
```

There are some cases:

1. `0` in the array.
2. Even number of negative numbers in the array.
3. Odd number of negative numbers in the array.

In case of Odd number of negative numbers in the array, we prefix product from left and right. 

If reach a `0` element, intialize the product base to `1`, so the prefix product will not keep to be `0` afterwords.

There is one corner case, the test sample does not cover, the prefix product could be out of Integer range!

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `nums`.

