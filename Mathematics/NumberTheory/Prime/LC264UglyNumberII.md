# LC264. Ugly Number II

### LeetCode

## Question

Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.

**Note that** 1 is typically treated as an ugly number, and n does not exceed 1690.

## Solutions

* C++1 (TLE)
```
class Solution {
public:
    vector<int> factors = {2,3,5};
    bool isUgly(int num)
    {
        for(int i=0; i<3; ++i)
        {
            if(num % factors[i] == 0)
            {
                num /= factors[i];
                i--;
            }
        }
        return num==1;
    }
    int nthUglyNumber(int n) {
        static vector<int> uglyNums(1,1);
        for(int i=uglyNums.back()+1; uglyNums.size()<n ; ++i)
        {
            if(isUgly(i)) 
            {
                uglyNums.push_back(i);
            }
        }
        return uglyNums[n-1];
    }
};
```

* C++2
```
int nthUglyNumber(int n) {
        vector<int> res(1,1);
        int p2=0, p3=0, p5=0;
        while(res.size()<n)
        {
            res.push_back(min(res[p2]*2, min(res[p3]*3, res[p5]*5)));
            if(res.back()==res[p2]*2) ++p2;
            if(res.back()==res[p3]*3) ++p3;
            if(res.back()==res[p5]*5) ++p5;
        }
        return res[n-1];
}
```

* C++3
```
int nthUglyNumber(int n) {
        static vector<int> uglyNums(1,1);
        static int two(0), three(0), five(0);
        while(uglyNums.size()<n)
        {
            int nextMin = min(uglyNums[two]*2, min(uglyNums[three]*3, uglyNums[five]*5));
            uglyNums.push_back(nextMin);
            if(uglyNums[two]*2 == nextMin) two++;
            if(uglyNums[three]*3 == nextMin) three++;
            if(uglyNums[five]*5 == nextMin) five++;
        }
        return uglyNums[n-1];
    }
```

## Explanation

Solution 1: calculate all ugly numbers from 1 to n (Time Limitation exceed)

Solution 2: Only count ugly numbers, `pi` record the previous location of multiply by i.

Solution 3: static method of solution 2.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)
