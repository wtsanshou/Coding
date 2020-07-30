# LC215. Kth Largest Element in an Array

### LeetCode

## Question

Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

**Example 1:**
```
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```

**Example 2:**
```
Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4
```

**Note:**
* You may assume k is always valid, 1 ≤ k ≤ array's length.

## Solutions

### Solution 1

* Python
```
def findKthLargest(self, nums: List[int], k: int) -> int:
    nums = sorted(nums)
    return nums[len(nums) - k]
```

**Explanation**

Sort the `nums` to know the location of Kth largest number.

**Complexity:**

* **worst-case time complexity:** `O(N*log(N)))`, where `N` is the length of `nums`.
* **worst-case space complexity:** `O(1)`.

### Solution 2

* Python
```
def findKthLargest(self, nums: List[int], k: int) -> int:
    pq = PriorityQueue()
    for num in nums:
        pq.put(num)
        if pq.qsize() > k:
            pq.get()
    return pq.get()
```

**Explanation**

Using a minHeap to keep top k largest numbers.

**Complexity:**

* **worst-case time complexity:** `O(N*log(K)))`, where `N` is the length of `nums`.
* **worst-case space complexity:** `O(K)`.

### Solution 3

* Python
```
def findKthLargest(self, nums: List[int], k: int) -> int:
    k = len(nums) - k
    i = 0
    j = len(nums) - 1
    while i < j:
        mid = self.partition(nums, i, j)
        if mid == k:
            return nums[mid]
        elif mid > k:
            j = mid - 1
        else:
            i = mid + 1
    return nums[k]
    
def partition(self, a:[], l: int, h: int):
    i = l + 1
    j = h
    while True:
        while (a[i] < a[l] and i < h):
            i += 1
        while (a[j] >= a[l] and j > l):
            j -= 1
        if (i >= j):
            break;
        
        self.swap(a, i, j)
    
    self.swap(a, l, j)
    return j

def swap(self, nums:[], i: int, j: int):
    temp = nums[i]
    nums[i] = nums[j]
    nums[j] = temp
```

**Explanation**

Based on the idea of Quick Sort, patition the `nums` until patition the k<sup>th</sup> element.

**Complexity:**

* **worst-case time complexity:** `O(N*log(N)))`, where `N` is the length of `nums`.
* **worst-case space complexity:** `O(1)`.