# LC189. Rotate Array

### LeetCode

## Question

Rotate an array of n elements to the right by k steps.

**For example**
```
with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].
```

**Follow up:**

* Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
* Could you do it in-place with O(1) extra space?

## Solutions

### Solution 1

* C++ (19ms) O(1)space  O(n) 
```
void rotate(vector<int>& nums, int k) {
    k = k%nums.size();
    reverse(nums.begin(), nums.end());
    reverse(nums.begin(), nums.begin()+k);
    reverse(nums.begin()+k, nums.end());
}
```

1. reverse the whole `nums`
2. reverse [0, k) of `nums`
3. reverse [k, nums.size) of `nums`

* **worst-case time complexity:** `O(N)`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(1)`

### Solution 2

* C++ (28ms) O(n)space O(n)
```
void rotate(vector<int>& nums, int k) {
    int len = nums.size();
    k = k%len;
    if(len<2 || k==0) return;
    
    // Make a copy of nums
    vector<int> numsCopy(nums.begin(), nums.end());
    
    // Rotate the elements.
    for (int i = 0; i < len; i++)
    {
        nums[(i + k)%len] = numsCopy[i];
    }
}
```

```
nums     0   1   2   3   4   5   6   7   8
copy             0   1   2   3   4   5   6   7   8
newId            3   4   5   6   7   8   0   1   2
```

* **worst-case time complexity:** `O(N)`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(N)`, where `N` is the size of the input `nums`.

### Solution 3

* C++ (44ms) O(1)space  O(n)
```
void rotate(vector<int>& nums, int k) {
    int len = nums.size();
    k = k%len;
    if(len<2 || k==0) return;
    reverse(nums.begin(), nums.begin() + (len-k));
    reverse(nums.begin()+ (len-k), nums.end());
    reverse(nums.begin(), nums.end());
}
```

1. reverse [0, len-k) of `nums`
2. reverse [len-k, nums.size) of `nums`
3. reverse the whole `nums`

* **worst-case time complexity:** `O(N)`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(1)`

### Solution 4

* Java (0ms) O(n)space O(n)
```
public void rotate(int[] nums, int k) {
    int n = nums.length;
    k = k%n;
    int[] temp = Arrays.copyOfRange(nums, 0, n-k);
    System.arraycopy(nums, n-k, nums, 0, k);
    System.arraycopy(temp, 0, nums, k, n-k); // n-k is the number of array elements to be copied. 
}
```

1. copy [0, len-k) of `nums` to [0, len-k) of `temp`
2. copy [len-k, len) of `nums` to [0, k) of `nums`
3. copy all of `temp` to [k, len] of `nums`

* **worst-case time complexity:** `O(N)`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(N)`, where `N` is the size of the input `nums`.