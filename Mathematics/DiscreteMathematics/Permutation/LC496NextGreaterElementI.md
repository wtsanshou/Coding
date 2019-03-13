# LC496. Next Greater Element I

### LeetCode

## Question

You are given two arrays (without duplicates) nums1 and nums2 where nums1’s elements are subset of nums2. Find all the next greater numbers for nums1's elements in the corresponding places of nums2.

The Next Greater Number of a number x in nums1 is the first greater number to its right in nums2. If it does not exist, output -1 for this number.

**Example 1:**
```
Input: nums1 = [4,1,2], nums2 = [1,3,4,2].
Output: [-1,3,-1]
Explanation:
    For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
    For number 1 in the first array, the next greater number for it in the second array is 3.
    For number 2 in the first array, there is no next greater number for it in the second array, so output -1.
```

**Example 2:**
```
Input: nums1 = [2,4], nums2 = [1,2,3,4].
Output: [3,-1]
Explanation:
    For number 2 in the first array, the next greater number for it in the second array is 3.
    For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
```

**Note:**

1.	All elements in nums1 and nums2 are unique.
2.	The length of both nums1 and nums2 would not exceed 1000.

## Solutions

### Solution 1

* C++ (9ms) O(mn)
```
class Solution {
public:
    int nextGreater(vector<int>& nums, int start, int val)
    {
        for(int i=start; i<nums.size(); ++i)
            if(nums[i]>val) return nums[i];
        return -1;
    }
    vector<int> nextGreaterElement(vector<int>& findNums, vector<int>& nums) {
        vector<int>res(findNums.size());
        unordered_map<int, int> addr;
        for(int i=0; i<nums.size(); ++i)
            addr[nums[i]] = i+1;
        for(int i=0; i<findNums.size(); ++i)
            res[i] = nextGreater(nums, addr[findNums[i]], findNums[i]);
        return res;
    }
};
```

* Python
```
def nextGreaterElement(self, findNums, nums):
    addr = dict([(nums[i],i) for i in range(len(nums))])
    return [self.getNextGreater(addr[findNums[i]], nums) for i in range(len(findNums))]

def getNextGreater(self, f, nums):
    for i in range(f+1, len(nums)):
        if nums[i] > nums[f]:
            return nums[i]
    return -1   
```

Using a normal map to map the numbers to their indexes in `nums`. Then find the next greater in the `nums`.

* **worst-case time complexity:** `O(N*M)`, where `N` is the length of the input `nums`, `M` is the length of the input `findNums`.
* **worst-case space complexity:** `O(N*M)`, where `N` is the length of the input `nums`, `M` is the length of the input `findNums`.
