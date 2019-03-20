# LC324. Wiggle Sort II

### LeetCode

## Question

Given an unsorted array nums, reorder it such that nums[0] < nums[1] > nums[2] < nums[3]....

**Example:**
```
(1) Given nums = [1, 5, 1, 1, 6, 4], one possible answer is [1, 4, 1, 5, 1, 6]. 
(2) Given nums = [1, 3, 2, 2, 3, 1], one possible answer is [2, 3, 1, 3, 1, 2].
```

**Note:**

* You may assume all input has valid answer.

**Follow Up:**

* Can you do it in O(n) time and/or in-place with O(1) extra space?

## Solutions 

### Solution 1

* C++
```
void wiggleSort(vector<int>& nums) {
    vector<int> sorted(nums);
    sort(sorted.begin(), sorted.end());
    for(int i = nums.size()-1, j=0, mid=i/2+1; i>=0; --i)
        nums[i] = sorted[i&1 ? mid++ : j++];
}
```

The idea is to sort the `nums`, and then put the left half small numbers in the `nums[i]` with even `i`, put the right large numbers in the `nums[i]` with odd `i`.

* **worst-case time complexity:** `O(Nlog(N))`, where `N` is the length of the `nums`.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the `nums`.

### Solution 2

* C++
```
void wiggleSort(vector<int>& nums) {
    int n = nums.size();
    nth_element(nums.begin(), nums.begin()+n/2, nums.end());
    int mid = nums[n/2];
    
    #define A(i) nums[(2*i+1)% (n|1)]
    
    int left=0, right=n-1, j=0;
    while(j<=right)
    {
        if(A(j) > mid)
            swap(A(left++), A(j++));
        else if(A(j) < mid)
            swap(A(j), A(right--));
        else
            j++;
    }
}
```

nth_element will partition the array `nums` to 3 part: `smaller numbers`, `the nth number`, and `larger numbers` 

The worst-case time complexity should be `O(Nlog(N))` although the average is `O(N)`.

`n|1`: make it odd number

`A(i)` read all odd locations first then all even locations.

**For example**

```
Accessing A(0) actually accesses nums[1].
Accessing A(1) actually accesses nums[3].
Accessing A(2) actually accesses nums[5].
Accessing A(3) actually accesses nums[7].
Accessing A(4) actually accesses nums[9].
Accessing A(5) actually accesses nums[0].
Accessing A(6) actually accesses nums[2].
Accessing A(7) actually accesses nums[4].
Accessing A(8) actually accesses nums[6].
Accessing A(9) actually accesses nums[8].
```

Always swap small odd `i` and large even `j`, or swap large odd `i` and small even `j`. Until the middle.

* **worst-case time complexity:** `O(Nlog(N))`, where `N` is the length of the `nums`.
* **worst-case space complexity:** `O(1)`.

