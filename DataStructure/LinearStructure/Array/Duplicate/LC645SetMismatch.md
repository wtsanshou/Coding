# LC645. Set Mismatch

### LeetCode

## Question

The set S originally contains numbers from 1 to n. But unfortunately, due to the data error, one of the numbers in the set got duplicated to another number in the set, which results in repetition of one number and loss of another number.

Given an array nums representing the data status of this set after the error. Your task is to firstly find the number occurs twice and then find the number that is missing. Return them in the form of an array.

**Example 1:**
```
Input: nums = [1,2,2,4]
Output: [2,3]
```

**Note:**

1.	The given array size will in the range [2, 10000].
2.	The given array's numbers won't have any order.

## Solutions

### Solution 1

* C++
```
vector<int> findErrorNums(vector<int>& nums) {
    int n = nums.size();
    vector<int> res(2), count(n);

    for(int num : nums)
        count[num-1]++;

    for(int i=1; i<=n; ++i)
    {
        if(count[i-1]==2) 
            res[0] = i;
        else if(count[i-1]==0)
            res[1] = i;
    }

    return res;
}
```

* Java
```
public int[] findErrorNums(int[] nums) {
    int n = nums.length;
    int[] count = new int[n];
    int[] res = new int[2];

    for(int num : nums){
        count[num-1]++;
        if(count[num-1]==2)
            res[0] = num;
    }

    for(int i=0; i<n; ++i)
        if(count[i]==0){
            res[1] = i+1;
            break;
        }

    return res;
}
```

#### Explanation

Since the given array size is not huge, we can use an array to count the numbers in the `nums`. The number occurs twice has record `2`, the missing number has record `0`.

* **worst-case time complexity:** `O(N)`, where `N` is the length of the input `nums`.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the input `nums`.

## Follow Up

* What if the given array size is unlimited?

### Solution 1

Sort the array `nums`.

* **worst-case time complexity:** `O(N*log(N))`, where `N` is the length of the input `nums`.
* **worst-case space complexity:** `O(log(N))`, where `N` is the length of the input `nums`.

### Solution 2

Using a set to find the duplicated number `x`. We can get `sum(1~N) = N*(N+1)/2` and `sum(nums)`. 

`diff` = `sum(1~N)` - `sum(nums)`.

the missing number is `x` + `diff`

* **worst-case time complexity:** `O(N)`, where `N` is the length of the input `nums`.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the input `nums`.
