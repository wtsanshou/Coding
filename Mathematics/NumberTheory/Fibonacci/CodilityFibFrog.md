# Codility. FibFrog

### Codility

## Question

The Fibonacci sequence is defined using the following recursive formula:

```
F(0) = 0 
F(1) = 1 
F(M) = F(M - 1) + F(M - 2) if M >= 2
```

A small frog wants to get to the other side of a river. The frog is initially located at one bank of the river (position −1) and wants to get to the other bank (position N). The frog can jump over any distance F(K), where F(K) is the K-th Fibonacci number. Luckily, there are many leaves on the river, and the frog can jump between the leaves, but only in the direction of the bank at position N.

The leaves on the river are represented in a zero-indexed array A consisting of N integers. Consecutive elements of array A represent consecutive positions from 0 to N − 1 on the river. Array A contains only 0s and/or 1s:

* 0 represents a position without a leaf;
* 1 represents a position containing a leaf.

The goal is to count the minimum number of jumps in which the frog can get to the other side of the river (from position −1 to position N). The frog can jump between positions −1 and N (the banks of the river) and every position containing a leaf.

For example, consider array A such that:

```
A[0] = 0 
A[1] = 0 
A[2] = 0 
A[3] = 1 
A[4] = 1 
A[5] = 0 
A[6] = 1 
A[7] = 0 
A[8] = 0 
A[9] = 0 
A[10] = 0
```

The frog can make three jumps of length F(5) = 5, F(3) = 2 and F(5) = 5.
Write a function:

`int solution(vector<int> &A);`

that, given a zero-indexed array A consisting of N integers, returns the minimum number of jumps by which the frog can get to the other side of the river. If the frog cannot reach the other side of the river, the function should return −1.

For example, given:

```
A[0] = 0 
A[1] = 0 
A[2] = 0 
A[3] = 1 
A[4] = 1 
A[5] = 0 
A[6] = 1 
A[7] = 0 
A[8] = 0 
A[9] = 0 
A[10] = 0
```

the function should return 3, as explained above.

Assume that:

* N is an integer within the range [0..100,000];
* each element of array A is an integer that can have one of the following values: 0, 1.

Complexity:

* expected worst-case time complexity is O(N*log(N));
* expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

* C++1
```
struct Point{
    int x;
    int step;
    Point(int a, int b) : x(a), step(b) {}
};
int solution(vector<int> &A) {
    int n = A.size();
    vector<int> fib(1);
    fib.push_back(1);
    for(int i=2; fib.back()<=n; ++i)
        fib.push_back(fib[i-1] + fib[i-2]);
    
    queue<Point> q ( {Point(-1, 0)} );
    while(!q.empty())
    {
        Point point = q.front();
        q.pop();
        for(unsigned int i = fib.size()-1; i>=2; --i)
        {
            int next = point.x + fib[i];
            if(next == n) return point.step + 1;
            if(next > n || next <0 || A[next]==0) continue;
            q.push(Point(next, point.step+1));
            A[next] = 0;
        }
    }
    return A.empty() ? 1 : -1;
}
```

## Explanation

1. Find all fibonacci numbers in [1, n]
2. Use a queue to record the positions of passed leaves. (Stack should work as well)
3. The passed leaf will be removed (set to `0`).
4. Move to next leaf when the next position `point.x + fib[i]` is less than n and containing a leaf
5. If the next position equals n, return `point.step + 1`.

## Testcase

 extreme_small_ones  empty array 

and all ones

extreme_small_zeros  all zeros

simple_functional  simple functional tests

small_random  small random test, length = ~100

small_cyclic  small cyclic test, length = ~500

small_fibonacci  small Fibonacci word test, length = 610

medium_random  medium random test, length = ~5,000

medium_thue_morse  medium Thue-Morse sequence, lenght = 2^13

large_big_result  large test with big result, length = ~100,000

large_cyclic  large cyclic test, length = ~100,000

large_random  large random test, length = ~100,000

extreme_large_ones_zeros  all zeros / ones, length = ~100,000
