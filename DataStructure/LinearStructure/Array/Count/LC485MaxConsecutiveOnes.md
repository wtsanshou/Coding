# LC485. Max Consecutive Ones

### LeetCode

## Question

Given a binary array, find the maximum number of consecutive 1s in this array.

**Example 1:**
```
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
The maximum number of consecutive 1s is 3.
```

**Note:**

* The input array will only contain 0 and 1.
* The length of input array is a positive integer and will not exceed 10,000

## Solution

### Solution 1

* C++ (46ms) O(n)
```
int findMaxConsecutiveOnes(vector<int>& nums) {
    int max1=0, cur=0;
    for(int num : nums)
    {
        if(num==0) cur=0;
        else
            max1 = max(max1, ++cur);
    }
    return max1;
}
```

* Python
```
def findMaxConsecutiveOnes(self, nums):
    res=0; count=0
    for num in nums:
        if num==0:
            res=max(res, count)
            count=0
        else:
            count += 1
    return max(res, count)
```

Just count the `consecutive 1s` in the array `nums`, and find the maximum number of `consecutive 1s`.

* **worst-case time complexity:** `O(n)`, where 'n' is the length of `nums`.
* **worst-case space complexity:** `O(n)`, where 'n' is the length of `nums`.