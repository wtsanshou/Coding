# LC89. Gray Code

### LeetCode

## Question

The gray code is a binary numeral system where two successive values differ in only one bit.

Given a non-negative integer n representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.
For example, given n = 2, return [0,1,3,2]. Its gray code sequence is:

```
00 - 0
01 - 1
11 - 3
10 - 2
```

**Note:**

For a given n, a gray code sequence is not uniquely defined.

For example, [0,2,3,1] is also a valid gray code sequence according to the above definition.

For now, the judge is able to judge based on one instance of gray code sequence. Sorry about that.

## Solutions

* C++1 (4ms) 
```
vector<int> grayCode(int n) {
    vector<int> res(1);
    for(int i=0; i<n; ++i)
        for(int j=res.size()-1; j>=0; --j)
            res.push_back(res[j] | (1<<i));
    return res;
}
```

* Java1 (3ms)
```
public List<Integer> grayCode(int n) {
    List<Integer> res = new ArrayList<Integer>();
    res.add(0);
    for(int i=0; i<n; ++i)
        for(int j=res.size()-1; j>=0; --j)
            res.add((res.get(j) | (1<<i)));
    return res;
}
```

## Explanation

List the result of gray code sequence:

```
0

0, 1

0, 1, 11, 10

0, 1, 11, 10, 110, 111, 101, 100

0, 1, 11, 10, 110, 111, 101, 100, 1100, 1101, 1111, 1110, 1010, 1011, 1001, 1000
.
.
.

```

From the gray code sequences, we can see that the current (n) gray code sequence is previous (n-1) gray code sequence + the revsersed previous (n-1) gray code sequence OR (1 << n-1).

Since the previous sequence is gray code sequence, the reversed previous (n-1) sequence is also gray code sequence. Only need to OR (1 << n-1) to make sure the middle two successive values differ in only one bit (the n-1 bit).

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(2<sup>n</sup>)
