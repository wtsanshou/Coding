# Codility. Min Perimeter Rectangle

### Codility

## Question

An integer N is given, representing the area of some rectangle.

The area of a rectangle whose sides are of length A and B is A * B, and the perimeter is 2 * (A + B).

The goal is to find the minimal perimeter of any rectangle whose area equals N. The sides of this rectangle should be only integers.

For example, given integer N = 30, rectangles of area 30 are:

* (1, 30), with a perimeter of 62,
* (2, 15), with a perimeter of 34,
* (3, 10), with a perimeter of 26,
* (5, 6), with a perimeter of 22.

Write a function:

int solution(int N);

that, given an integer N, returns the minimal perimeter of any rectangle whose area is exactly equal to N.

For example, given an integer N = 30, the function should return 22, as explained above.

**Assume that:**

* N is an integer within the range [1..1,000,000,000].

**Complexity:**

* expected worst-case time complexity is O(sqrt(N));
* expected worst-case space complexity is O(1).

## Solutions

* C++1
```
int solution(int N) {
    int sq = sqrt(N);
    for(int i=sq; i>1; --i)
        if(N%i == 0) return 2*(i + N/i);
    return 2*(1+N);
}
```

* Java
```
public int solution(int N) {
    // write your code in Java SE 8
    int n = (int)Math.sqrt((double)N);
    for(int i=n; i>0; i--)
        if(N%i == 0)
            return 2 * (i + (N/i));
    return 1;
}
```

## Testcase

extreme_min  N = 1 test

simple1  N = 36 test

simple2  N = 48 test

simple3  N = 101 test

small  N = 1,234 test

medium  N = 4,564,320 test

prime1  N = 15,486,451 test

square  N = 100,000,000 test

prime2  N = 982,451,653 test

extreme_max  N = 1,000,000,000 test


