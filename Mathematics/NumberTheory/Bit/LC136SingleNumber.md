# LC136. Single Number

### LeetCode

## Question

Given an array of integers, every element appears twice except for one. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

## Solutions

* C++1 (16ms)
```
int singleNumber(vector<int>& nums) {
    for(int i=1; i<nums.size(); ++i)
        nums[0] ^= nums[i];
    return nums[0];
}
```

* python
```
def singleNumber(self, nums):
    for i in range(1,len(nums)):
        nums[0] ^= nums[i]
    return nums[0]
```

* Bash1
```bash
#!/bin/bash
read N
array=($(cat))
res=0
for i in ${array[@]}
do
    res=$(( $res ^ $i ))
done
echo $res
```

* Bash2
```bash
#!/bin/bash
read N
array=($(cat))
array=${array[@]}
echo $((${array// /^}))
```

## Explanation

The same number ^ the same number = 0

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)