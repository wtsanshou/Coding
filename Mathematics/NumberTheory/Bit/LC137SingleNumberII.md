# LC137. Single Number II

### LeetCode

## Question

Given an array of integers, every element appears three times except for one, which appears exactly once. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

## Solutions

* C++1 (12ms) O(32n)
```
int singleNumber(vector<int>& nums) {
        int res = 0;
        for(int i=0; i<=31; ++i)
        {
            int sum = 0;
            for(auto num : nums)
                if((num & (1<<i)) != 0)
                    sum++;
            sum %= 3;
            res |= (sum << i);
        }
        return res;
}
```

* C++2 (12ms) 
```
int singleNumber(vector<int>& nums) {
        int ones=0, twos =0;
        for(int n : nums)
        {
            ones = (ones ^ n) & ~twos;
            twos = (twos ^ n) & ~ones;
        }
        return ones;
}
```

* Java1 (6ms)
```
public int singleNumber(int[] nums) {
        int res=0;
        for(int i=0; i<32; ++i)
        {
            int count = 0;
            int bit = 1<<i;
            for(int num : nums)
                if((bit & num) != 0)
                    count++;
            if(count%3 != 0)
                res += bit;
        }
        return res;
}
```

## Explanation

The usual bit manipulation code is bit hard to get and replicate. I like to think about the number in 32 bits and just count how many 1s are there in each bit, and `sum %= 3` will clear it once it reaches 3. After running for all the numbers for each bit, if we have a 1, then that 1 belongs to the single number, we can simply move it back to its spot by doing `res |= sum << i`;
This has complexity of O(32n), which is essentially O(n) and very easy to think and implement. Plus, you get a general solution for any times of occurrence. Say all the numbers have 5 times, just do `sum %= 5`.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)

## Testcase:

* 1

**Input**
```
[1,1,2,3,3,4,1,2,2,3]
```

**Output**
```
4
```


* 2

**Input**
```
[-1,-1,2,3,3,-4,-1,2,2,3]
```

**Output**
```
-4
```





