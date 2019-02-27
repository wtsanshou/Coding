# LC238. Product of Array Except Self

### LeetCode

## Question

Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Solve it without division and in O(n).

**For example**
```
given [1,2,3,4], return [24,12,8,6].
```

**Follow up:** 

* Could you solve it with constant space complexity? (Note: The output array does not count as extra space for the purpose of space complexity analysis.)

## Solutions

### Solution 1

* C++1 (76ms) O(n)
```
vector<int> productExceptSelf(vector<int>& nums) {
    int temp = 1, n=nums.size();
    vector<int> res(n, 1);
    for(int i=1; i<n; ++i)
        res[i] = res[i-1]*nums[i-1];
    for(int i=n-2; i>=0; --i)
    {
        temp *= nums[i+1];
        res[i] = res[i] * temp;
    }
    return res;
}
```

* C++2 (64ms)
```
vector<int> productExceptSelf(vector<int>& nums) {
    int fromBegin = 1, fromEnd = 1, len = nums.size();
    vector<int> res(len, 1);
    for(int i=0; i<len; ++i)
    {
        res[i] *= fromBegin;
        fromBegin *= nums[i];
        res[len-i-1] *= fromEnd;
        fromEnd *= nums[len-i-1];
    }
    return res;
}
```

* Java (4ms)
```
public int[] productExceptSelf(int[] nums) {
    int len = nums.length;
    int [] res = new int[len];
    Arrays.fill(res, 1);
    for(int i=1; i<len; ++i)
    {
        res[i] = res[i-1] * nums[i-1];
    }
    int right=1;
    for(int i=len-1; i>=0; --i)
    {
        res[i] *= right;
        right *= nums[i];
    }
    return res;
}
```

The first idea I had is to product all numbers in the `nums`, and then divided by `nums[i]` to get `output[i]`. But this solution missed the corner case: number could be `0`.

The numbers in the test cases must be small enough, otherwise it is very easy to overflow Integer when product `n-1` numbers.

The idea is to get:
1. `left[i]` = product of all left numbers of `nums[i]`
2. `right[i]` = product of all right numbers  of `nums[i]`
3. `output[i]` = `left[i]` * `right[i]`

* **worst-case time complexity:** `O(n)`, where 'n' is the length of `nums`.
* **worst-case space complexity:** `O(n)`, where 'n' is the length of `nums`.
