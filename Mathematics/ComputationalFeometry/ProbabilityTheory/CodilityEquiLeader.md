# Codility. Equi Leader

### LeetCode

## Question

A non-empty zero-indexed array A consisting of N integers is given.
The leader of this array is the value that occurs in more than half of the elements of A.

An equi leader is an index S such that 0 ≤ S < N − 1 and two sequences A[0], A[1], ..., A[S] and A[S + 1], A[S + 2], ..., A[N − 1] have leaders of the same value.

For example, given array A such that:

```
A[0] = 4 
A[1] = 3 
A[2] = 4 
A[3] = 4 
A[4] = 4 
A[5] = 2
```

we can find two equi leaders:

* 0, because sequences: (4) and (3, 4, 4, 4, 2) have the same leader, whose value is 4.
* 2, because sequences: (4, 3, 4) and (4, 4, 2) have the same leader, whose value is 4.

The goal is to count the number of equi leaders.

Write a function:

`int solution(vector<int> &A);`

that, given a non-empty zero-indexed array A consisting of N integers, returns the number of equi leaders.

For example, given:

```
A[0] = 4 
A[1] = 3 
A[2] = 4 
A[3] = 4 
A[4] = 4 
A[5] = 2
```

the function should return 2, as explained above.

**Assume that:**

* N is an integer within the range [1..100,000];
* each element of array A is an integer within the range [−1,000,000,000..1,000,000,000].

**Complexity:**

* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

* C++1
```
int solution(vector<int> &A) {
    int leader=0, count=0;
    for(int a : A)
    {
        if(count==0)
        {
            leader = a;
            count++;
        }
        else if(leader==a) count++;
        else count--;
    }
    
    int n = A.size();
    vector<bool> LR(n);
    vector<bool> RL(n);
    int lr =0, rl = 0;
    for(int i=0; i<n-1; ++i)
    {
        if(A[i]==leader) lr++;
        if(A[n-i-1]==leader) rl++;
        int half = (i+1)/2;
        if(lr>half) LR[i] = true;
        if(rl>half) RL[n-i-1] = true;
    }
    
    int res = 0;
    for(int i=0; i<n-1; ++i)
        if(LR[i] && RL[i+1])
            res++;
    return res;
}
```

* C++2
```
int solution(vector<int> &A) {
    int leader=0, count=0;
    for(int a : A)
    {
        if(count==0)
        {
            leader = a;
            count++;
        }
        else if(leader==a) count++;
        else count--;
    }
    
    int n = A.size()-1;
    vector<bool> LR(n);
    vector<bool> RL(n);
    int lr =0, rl = 0;
    for(int i=0; i<n; ++i)
    {
        if(A[i]==leader) lr++;
        if(A[n-i]==leader) rl++;
        int half = (i+1)/2;
        if(lr>half) LR[i] = true;
        if(rl>half) RL[n-i-1] = true;
    }
    
    int res = 0;
    for(int i=0; i<n; ++i)
        if(LR[i] && RL[i])
            res++;
    return res;
}
```

## Explanation

The equi leader is the majority element of the array.

1. Find the majority element using Moore Voting algorithm.
2. Count the majority element from each side of the array.
3. If more than half of each side, mark it.
4. Count the number of marked by both sides.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)

## Testcase

single  single element

double  two elements

simple  simple test

small_random  small random test with two values, length = ~100

small  random + 200 * [MIN_INT] + random ,length = ~300

large_random  large random test with two values, length = ~50,000

large  random(0,1) + 50000 * [0] + random(0, 1), length = ~100,000

large_range  1, 2, ..., N, length = ~100,000

extreme_large  all the same values
