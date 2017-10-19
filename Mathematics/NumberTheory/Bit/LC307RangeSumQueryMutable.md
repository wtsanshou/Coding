# LC307. Range Sum Query – Mutable

### LeetCode

## Question

Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

The update(i, val) function modifies nums by updating the element at index i to val.

**Example:**

```
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```

**Note:**

* The array is only modifiable by the update function.
* You may assume the number of calls to update and sumRange function is distributed evenly.

## Solutions

* C++1 (TLE)
```
class NumArray {
private: 
    vector<int> nums;
    vector<int> sums;
public:
    NumArray(vector<int> nums) {
        this->nums = nums;
        sums = vector<int>(nums.size()+1);
        for(int i=nums.size()-1; i>=0; --i)
            sums[i] = nums[i] + sums[i+1];
    }
    
    void update(int i, int val) {
        int change = val - nums[i];
        nums[i] = val;
        for(int k=i; k>=0; --k)
            sums[k] += change;
    }
    
    int sumRange(int i, int j) {
        return sums[i] - sums[j+1];
    }
};
```

* C++2
```
class NumArray {
private:
    vector<int> BIT;
    vector<int> Nums;
public:
    NumArray(vector<int> &nums){
        int n = nums.size();
        Nums = nums;
        //BIT = vector<int>(n+1);
        BIT.resize(n+1);
        for(int i=0; i<n; ++i)
        {
            updateBIT(i, nums[i]);
        }
    }

    void update(int i, int val) {
        if(val != Nums[i])
        {
            updateBIT(i, val-Nums[i]);
            Nums[i] = val;
        }
    }

    int sumRange(int i, int j) {
        return leftSum(j) - leftSum(i-1);
    }
    
    int leftSum(int i)
    {
        i++;
        int sum=0;
        while(i>0)
        {
            sum += BIT[i];
            i -= i & (-i);
        }
        return sum;
    }
    
    void updateBIT(int i, int val)
    {
        i++;
        while(i<BIT.size())
        {
            BIT[i] +=val;
            i += i & (-i); //double the last bit
        }
    }
};
```

## Explanation

Solution1: the straight forward way, update the left sum of all positions.

* **Update worst-case time complexity:** O(n)
* **sumRange worst-case time complexity:** O(1)
* **worst-case space complexity:** O(n)

Solution2: the complex way

See <a href="https://www.topcoder.com/community/data-science/data-science-tutorials/binary-indexed-trees/">Binary Indexed Trees</a>

**Example:** 

given an array a[0]...a[7], we use a array BIT[9] to represent a tree, where index [2] is the parent of [1] and [3], [6] is the parent of [5] and [7], [4] is the parent of [2] and [6], and [8] is the parent of [4]. I.e.,

```
     * BIT[] as a binary tree:
     *            ______________*
     *            ______*
     *            __*     __*
     *            *   *   *   *
     * indices: 0 1 2 3 4 5 6 7 8
```

**Where:** `i & (-i)` means only keeping the most right `1` bit

```
number               0000 0000 0000 0000 0000 0000 0101 1100
~number              1111 1111 1111 1111 1111 1111 1010 0011
(~number) + 1        1111 1111 1111 1111 1111 1111 1010 0100
-number              1111 1111 1111 1111 1111 1111 1010 0100
(number) & (-number) 0000 0000 0000 0000 0000 0000 0000 0100
```

* **Update worst-case time complexity:** O(log(n))
* **sumRange worst-case time complexity:** O(1)
* **worst-case space complexity:** O(n)