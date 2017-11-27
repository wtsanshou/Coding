# LC268. Missing Number

### LeetCode

## Question

Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

**For example**,  Given nums = [0, 1, 3] return 2.

**NOTE:** 

Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

## Solutions

* C++1 (36ms)
```
int missingNumber(vector<int>& nums) {
    int len = nums.size();
    int sumN = len*(len+1)/2;
    for(int n : nums) sumN -= n;
    return sumN;
}
```

* Java1 (1ms)
```
public int missingNumber(int[] nums) {
    int n = nums.length;
    int sum = 0;
    for(int num : nums)
        sum += num;
    return n*(n+1)/2 - sum;
}
```

## Explanation

If there is no missing number in the array, the sum of the array is `n*(n+1)/2`. Therefore, `the missing number` equals `n*(n+1)/2` minus `the actural sum of the array`.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)