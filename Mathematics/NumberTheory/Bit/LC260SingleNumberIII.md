# LC260. Single Number III

### LeetCode

## Question

Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

**For example:**

Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].

**Note:**

1. The order of the result is not important. So in the above example, [5, 3] is also correct.
2. Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?

## Solutions

* C++1 (16ms) O(n)
```
vector<int> singleNumber(vector<int>& nums) {
    int key = 0;
    vector<int> res(2, 0);
    for(int num : nums)
        key ^= num;
    key = key & (~(key-1));
    for(int num : nums)
    {
        if((num & key) != 0)
            res[0] ^= num;
        else res[1] ^= num;
    }
    return res;
}
```

## Explanation

1. find the bitwise NOT (key) of the two elements that appear only once. **NOTE:** num ^ num = 0.
2. find the location of a bit in the key. One element has `1` in the location of the bit, another has `0` in the location of the bit.
3. travel all the numbers, bitwise NOT two groups of numbers (one group of numbers have `1` in the location of the bit, another group of numbers have `0` in the location of the bit).

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)

## Testcase**

* 1

**input:** [1,1,2,3,3,4]

**output:** [2,4]

* 2

**input:** [-1,-1,2,3,3,-4]

**output:** [2,-4]

