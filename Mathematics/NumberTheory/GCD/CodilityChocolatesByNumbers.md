# Codility. ChocolatesByNumbers

### Codility

## Question

Two positive integers N and M are given. Integer N represents the number of chocolates arranged in a circle, numbered from 0 to N − 1.

You start to eat the chocolates. After eating a chocolate you leave only a wrapper.

You begin with eating chocolate number 0. Then you omit the next M − 1 chocolates or wrappers on the circle, and eat the following one.

More precisely, if you ate chocolate number X, then you will next eat the chocolate with number (X + M) modulo N (remainder of division).

You stop eating when you encounter an empty wrapper.

For example, given integers N = 10 and M = 4. You will eat the following chocolates: 0, 4, 8, 2, 6.

The goal is to count the number of chocolates that you will eat, following the above rules.

Write a function:

int solution(int N, int M);

that, given two positive integers N and M, returns the number of chocolates that you will eat.

For example, given integers N = 10 and M = 4. the function should return 5, as explained above.

Assume that:

* N and M are integers within the range [1..1,000,000,000].
Complexity:
* expected worst-case time complexity is O(log(N+M));
* expected worst-case space complexity is O(log(N+M)).

## Solutions

* C++1 (75%)
```
#include <unordered_map>
// you can write to stdout for debugging purposes, e.g.
// cout << "this is a debug message" << endl;

std::unordered_map<int, bool> map;

int myRecursive(int start, int N, int M)
{
    if(map[start]) return 0;
    map[start] = true;
    return myRecursive((start+M)%N, N, M) + 1;
}

int solution(int N, int M) {
    // write your code in C++14 (g++ 6.2.0)
    if(M==1) return N;
    return myRecursive(0, N, M);
}
```

* C++2 
```
int GCD(int N, int M)
{
    if(N < M) return GCD(M, N);
    if(M==0) return N;
    return GCD(M, N%M);
}

int solution(int N, int M) {
    // write your code in C++14 (g++ 6.2.0)
    return N / GCD(N, M);
}
```

* C++3
```
int GCD(int N, int M)
{
    return (M==0) ? N : GCD(M, N%M);
}

int solution(int N, int M) {
    // write your code in C++14 (g++ 6.2.0)
    return N / GCD(N, M);
}
```

* Java1
```
class Solution {
    public int gcd(int a, int b) {
        if ((a % b) == 0) {
            return b;
        } else {
            return gcd(b, a % b);
        }
    }

    public int solution(int N, int M) {
        return N / gcd(N, M);
    }
}
```

## Explanation

Solution1: Using a map to record if the position is chocolate (false) or wrapper(true). If the position is chocolate, eat it and use recursive to check the next position (`(start+M)%N`).

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)

Solution2: Using <a href="https://en.wikipedia.org/wiki/Greatest_common_divisor">Greatest Common Divisor (GCD)</a>

only (`(N / GCD(N, M))` * M) % N == 0

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)
