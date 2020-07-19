# LC1389. Create Target Array in the Given Order

### LeetCode

## Quesiton

Given two arrays of integers nums and index. Your task is to create target array under the following rules:

Initially target array is empty.
From left to right read nums[i] and index[i], insert at index index[i] the value nums[i] in target array.
Repeat the previous step until there are no elements to read in nums and index.
Return the target array.

It is guaranteed that the insertion operations will be valid.

**Example 1:**
```
Input: nums = [0,1,2,3,4], index = [0,1,2,2,1]

Output: [0,4,1,3,2]

Explanation:
nums       index     target
0            0        [0]
1            1        [0,1]
2            2        [0,1,2]
3            2        [0,1,3,2]
4            1        [0,4,1,3,2]
```

**Example 2:**
```
Input: nums = [1,2,3,4,0], index = [0,1,2,3,0]

Output: [0,1,2,3,4]

Explanation:
nums       index     target
1            0        [1]
2            1        [1,2]
3            2        [1,2,3]
4            3        [1,2,3,4]
0            0        [0,1,2,3,4]
```

**Example 3:**
```
Input: nums = [1], index = [0]

Output: [1]
```

**Constraints:**

* 1 <= nums.length, index.length <= 100
* nums.length == index.length
* 0 <= nums[i] <= 100
* 0 <= index[i] <= i

## Solutions

### Soltuion 1

* Python
```
def createTargetArray(self, nums: List[int], index: List[int]) -> List[int]:
    hashmap = {}
    for i in range(len(nums)):
        if index[i] < i:
            self.move_right_index(hashmap, i, index)
        hashmap[index[i]] = nums[i]
        
    return [item[1] for item in sorted(hashmap.items())]
    
def move_right_index(self, hashmap: {}, i: int, index: List[int]):
    for j in range(i, index[i], -1):
        hashmap[j] = hashmap.get(j - 1) 
```

## Explanation

It's like insert values into a list. I am using dict to implement it. If we build a linked list, it might be faster. But the worst case complexity is the same as my solution.

* **worst-case time complexity:** O(N<sup>2</sup>), `N` is the length the list `nums`.
* **worst-case space complexity:** `O(N)`, `N` is the length the list `nums`.
