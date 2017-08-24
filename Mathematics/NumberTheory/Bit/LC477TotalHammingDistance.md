# LC477. Total Hamming Distance

### LeetCode

## Question

The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Now your job is to find the total Hamming distance between all pairs of the given numbers.

Example:

Input: 4, 14, 2

Output: 6

Explanation: In binary representation, the 4 is 0100, 14 is 1110, and 2 is 0010 (just showing the four bits relevant in this case). So the answer will be:

HammingDistance(4, 14) + HammingDistance(4, 2) + HammingDistance(14, 2) = 2 + 2 + 2 = 6.

Note:

1. Elements of the given array are in the range of 0 to 10<sup>9</sup>
2. Length of the array will not exceed 10<sup>4</sup>.

## Solutions

* C++1 (TLE)
```
class Solution {
public:
    int Hamming(int a, int b)
    {
        int res = 0;
        while(a!=0 || b!=0)
        {
            res += (a&1) ^ (b&1);
            a >>= 1;
            b >>= 1;
        }
        return res;
    }
    int totalHammingDistance(vector<int>& nums) {
        int n = nums.size();
        if(n<=1) return 0;
        vector<int>dp(n);
        for(int i=1; i<n; ++i)
        {
            for(int j=i-1; j>=0; --j)
                dp[i-1] += Hamming(nums[i], nums[j]); 
            dp[i] = dp[i-1];
        }
        return dp[n-1];
    }
};
```

* C++2 (82ms)
```
int totalHammingDistance(vector<int>& nums) {
        int n = nums.size();
        if(n<=1) return 0;
        int res = 0;
        for(int i=0; i<32; ++i)
        {
            int count1 = 0;
            for(auto num : nums)
                count1 += (num>>i) & 1;
            res += count1 * (n - count1);
        }
        return res;
    }
```

## Explanation

**Solution1:** Using dynamic programming to record previous total hamming distance (`dp[i-1]` i.e. the total hamming distance without nums[i]). Then, calculate the `sum` of hamming distance between nums[i] and (nums[0]~nums[i-1]). Finally, the result is `dp[i-1]` + `sum`.

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(n)

**Soultion2:** Count the number of `1` in each bit. The total hamming distance of each bit is (number of `1`) * (number of `0`). The final total hamming distance of the nums is the sum of the total hamming distance of each bit.

* **worst-case time complexity:** O(32n)
* **worst-case space complexity:** O(1)