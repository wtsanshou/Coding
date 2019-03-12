# LC31. Next Permutation

### LeetCode

## Question

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place, do not allocate extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

## Solutions

### Solution 1

* C++
```
void nextPermutation(vector<int>& nums) {
    int n = nums.size();
    int i=n-2;
    while(i>=0 && nums[i]>=nums[i+1])
        i--;
    if(i==-1) 
    {
        reverse(nums.begin(), nums.end());
        return;
    }
    int j = i+1;
    for(; j<n-1; ++j) //O(n)
        if(nums[i]<nums[j] && nums[i]>=nums[j+1])
            break;
    swap(nums[i], nums[j]);
    reverse(nums.begin()+i+1, nums.end());
}
```

1. From back to front, find the first ascending number's location `i`.
2. in the number after `i`, find the location `j` of a number who is larger or equal the number in `i`. If no this number, the location of the last number in the array `nums` is `j`.
3. swap the numbers in `i` and `j`.
4. reverse the numbers after the location of `i`.

```
    6   7   *3   5   4    2   1
->  6   7   *3   5   4   *2   1
->  6   7   *2   5   4   *3   1
->  6   7    2   1   3    4   5
```

* **worst-case time complexity:** `O(N)`, where `N` is the length of the input `nums`.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the input `nums`.

### Solution 2

* C++
```
void nextPermutation(vector<int>& nums) {
    if(nums.empty()) return;
    int i=nums.size()-2;
    while(i>=0 && nums[i]>=nums[i+1]) i--;
    reverse(nums.begin()+i+1,nums.end());
    if(i==-1) return;
    auto it = upper_bound(nums.begin()+i+1,nums.end(), nums[i]); //O(log(n))
    swap(nums[i], *it);
}
```

1. From back to front, find the first ascending number's location `i`.
2. reverse the numbers after the location of `i`.
3. find the upper bound of `nums[i]` in the numbers after `i`.
4. swap the numbers in `i` and `j`.

```
    6   7   *3   5    4    2   1
->  6   7   *3   1    2    4   5
->  6   7   *3   1   *2    4   5
->  6   7    2   1    3    4   5
```

* **worst-case time complexity:** `O(N)`, where `N` is the length of the input `nums`.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the input `nums`.
