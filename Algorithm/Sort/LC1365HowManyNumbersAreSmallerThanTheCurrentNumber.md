# LC1365. How Many Numbers Are Smaller Than the Current Number

### LeetCode

## Question

Given the array nums, for each nums[i] find out how many numbers in the array are smaller than it. That is, for each nums[i] you have to count the number of valid j's such that j != i and nums[j] < nums[i].

Return the answer in an array.

**Example 1:**

```
Input: nums = [8,1,2,2,3]
Output: [4,0,1,1,3]

Explanation: 
For nums[0]=8 there exist four smaller numbers than it (1, 2, 2 and 3). 
For nums[1]=1 does not exist any smaller number than it.
For nums[2]=2 there exist one smaller number than it (1). 
For nums[3]=2 there exist one smaller number than it (1). 
For nums[4]=3 there exist three smaller numbers than it (1, 2 and 2).
```

**Example 2:**

```
Input: nums = [6,5,4,8]
Output: [2,1,0,3]
```

**Example 3:**

```
Input: nums = [7,7,7,7]
Output: [0,0,0,0]
```

## Solutions

### Solution 1

* Python

```
def smallerNumbersThanCurrent(self, nums: List[int]) -> List[int]:
    sorted_list = sorted(nums)
    nums_map = {}
    for i in range(len(sorted_list)):
        if nums_map.get(sorted_list[i]) is None:
            nums_map[sorted_list[i]] = i
    return list(map(lambda x: nums_map[x], nums))
```

## Explanation

The most straight forward idea is to for loop each number `nums[i]`, count how many numbers in the array are smaller than `nums[i]`. The solutions O(n<sup>2</sup>) time complexity. Is there a faster solution?

If the list `nums` is a sorted list, it will be very easy to count the smaller numbers. The index `i` of the sorted list is the count of smaller numbers for `nums[i]`. We can use a hashmap to remember the count of smallers numbers for each number. Here, we need to consider the duplicated numbers in the list. Because the question is asking for smaller than, we only need to put the first duplicated number index into the map.


* **worst-case time complexity:** `O(N*log(N))`, where `N` is the length of the list `nums`.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the list `nums`.


