# LC421. Maximum XOR of Two Numbers in an Array

### LeetCode

## Question

Given a non-empty array of numbers, a<sub>0</sub>, a<sub>1</sub>, a<sub>2</sub>, … , a<sub>n-1</sub>, where 0 ≤ a<sub>i</sub> < 2<sup>31</sup>.

Find the maximum result of a<sub>i</sub> XOR a<sub>j</sub>, where 0 ≤ i, j < n.
Could you do this in O(n) runtime?

**Example:**

**Input:** [3, 10, 5, 25, 2, 8]

**Output:** 28

**Explanation:** The maximum result is 5 ^ 25 = 28.

## Solutions

* C++1 (TLE) 
```
int findMaximumXOR(vector<int>& nums) {
    int maxV = 0;
    for(int i=0; i<nums.size(); ++i)
        for(int j=i+1; j<nums.size(); ++j)
            maxV = max(maxV, nums[i] xor nums[j]);
    return maxV;
}
```

* C++2 
```
int findMaximumXOR(vector<int>& nums) {
    int max=0, mask=0;
    for(int i=31; i>=0; --i)
    {
        mask |= 1<<i;
        unordered_set<int> set;
        for(int num : nums)
            set.insert(num & mask);
        
        int temp = max | 1<<i;
        for(int profix : set)
        {
            if(set.count(profix ^ temp)>0)
            {
                max = temp;
                break;
            }
        }
    }
    return max;
}
```

## Explanation

**Solution 1** the straight forward way is to check every two pairs of numbers in the array

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(1)

**Solution 2** Check the prefixs one bit by one bit from highest bit to lowest bit in the array. every time add 1 bit to the maximum result, and check if the maximum result is from two numbers in the array.

**NOTE :** `A ^ B = C`  --> `B ^ C = A`  --> `A ^ C = B`

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)


