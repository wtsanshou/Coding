# LC523. Continuous Subarray Sum

### LeetCode

## Question

Given a list of non-negative numbers and a target integer k, write a function to check if the array has a continuous subarray of size at least 2 that sums up to the multiple of k, that is, sums up to n*k where n is also an integer.

**Example 1:**
```
Input: [23, 2, 4, 6, 7],  k=6
Output: True
Explanation: Because [2, 4] is a continuous subarray of size 2 and sums up to 6.
```

**Example 2:**
```
Input: [23, 2, 6, 4, 7],  k=6
Output: True
Explanation: Because [23, 2, 6, 4, 7] is an continuous subarray of size 5 and sums up to 42.
```

**Note:**
1. The length of the array won't exceed 10,000.
2. You may assume the sum of all the numbers is in the range of a signed 32-bit integer.

## Solutions

### Solution 1

* C++ (56ms)
```
bool checkSubarraySum(vector<int>& nums, int k) {
    vector<int> sumNums(nums.begin(), nums.end());
    
    for(int j=1; j<nums.size(); ++j)
    {
        for(int i=0;i+j<nums.size(); ++i)
        {
            sumNums[i] += nums[i+j];
            if(k==0)
            { 
                if(sumNums[i]==0) return true;
            }
            else if(sumNums[i]%k == 0) return true;
        }
    }
    return false;
}
```

Using an array to store the SubarraySum `sumNums` which is starting from each `i` int the `nums`.

Aggregate the one right number to the `sumNums` each time and check if it is sumed up to `n*k`.

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the `nums`.
* **worst-case space complexity:** O(n), where `n` is the length of the `nums`.
