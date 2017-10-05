# Codility. Binary Gap

### Codility

## Question

A binary gap within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps.

Write a function:

int solution(int N);

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5.

Assume that:

N is an integer within the range [1..2,147,483,647].

Complexity:

* expected worst-case time complexity is O(log(N));
* expected worst-case space complexity is O(1).

## Solutions

* C++1 (100%)
```
#include <algorithm>
// you can write to stdout for debugging purposes, e.g.
// cout << "this is a debug message" << endl;
int solution(int N) {
    // write your code in C++14 (g++ 6.2.0)
    int oneP = -1, res=0;
    for(int i=0; i<32; ++i)
        if(((1<<i)&N) >0)
        {
            if(oneP>=0) res = max(res, i-oneP-1);
            oneP = i;
        }
    return res;
}
```

## Explanation

Remember the previous 1's position in the number N. If found a `1` (except the first `1`), calculate a gap.
