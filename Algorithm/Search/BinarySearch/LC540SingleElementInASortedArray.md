# LC540. Single Element in a Sorted Array

### LeetCode

## Question

Given a sorted array consisting of only integers where every element appears twice except for one element which appears once. Find this single element that appears only once.

**Example 1:**

```
Input: [1,1,2,3,3,4,4,8,8]
Output: 2
```

**Example 2:**

```
Input: [3,3,7,7,10,11,11]
Output: 10
```

**Note:** Your solution should run in O(log n) time and O(1) space.

## Solutions

* C#1 (172ms)
```
public int SingleNonDuplicate(int[] nums) {
        int i=0, j=nums.Length-1;
        while(i < j){
            int mid = i + (j-i)/2;
            if(nums[mid]!=nums[mid-1] && nums[mid]!=nums[mid+1])
                return nums[mid];
            if(mid % 2 == 0){
                if(nums[mid] == nums[mid-1]) j = mid;
                else i = mid;
            }
            else{
                if(nums[mid] == nums[mid-1]) i = mid+1;
                else j = mid-1;
            }
        }
        return nums[i];
    }
```

* C#2 (179ms)
```
public int SingleNonDuplicate(int[] nums) {
        int i=0, j=nums.Length-1;
        while(i < j){
            int mid = i + (j-i)/2;
            if(mid % 2 == 0){
                if(nums[mid] == nums[mid-1]) j = mid;
                else i = mid;
            }
            else{
                if(nums[mid] == nums[mid-1]) i = mid+1;
                else j = mid-1;
            }
        }
        return nums[i];
    }
```

* C#3 (138ms) (Beat 100%)
```
public int SingleNonDuplicate(int[] nums) {
        int i=0, j=nums.Length-1;
        while(i < j){
            int mid = i + (j-i)/2;
            if(nums[mid] == nums[mid-1]){
                if(mid % 2 == 0) j = mid;
                else i = mid+1;
            }
            else{
                if(mid % 2 == 0) i = mid;
                else j = mid-1;
            }
        }
        return nums[i];
    }
```

## Explanation

At the first view, it looks like the old question <a href="../../../Mathematics/NumberTheory/Bit/LC136SingleNumber.md">LC136. Single Number</a>. But then I saw the array is sorted, and the solution should run in O(log n) time and O(1) space. I can guess the solution is binary search algorithm.

There are two cases:

+ When the middle index is even

- If the middle value equals left value, the target is in the left
- If the middle value equals right value, the target is in the right

+ When the middle index is odd

- If the middle value equals left value, the target is in the right
- If the middle value equals right value, the target is in the left

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)
