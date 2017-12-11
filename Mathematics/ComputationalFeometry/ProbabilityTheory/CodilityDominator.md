# Codility. Dominator

### Codility

## Question

A zero-indexed array A consisting of N integers is given. The dominator of array A is the value that occurs in more than half of the elements of A.
For example, consider array A such that

```
A[0] = 3 
A[1] = 4 
A[2] = 3 
A[3] = 2 
A[4] = 3 
A[5] = -1 
A[6] = 3 
A[7] = 3
```

The dominator of A is 3 because it occurs in 5 out of 8 elements of A (namely in those with indices 0, 2, 4, 6 and 7) and 5 is more than a half of 8.

Write a function

`int solution(vector<int> &A);`

that, given a zero-indexed array A consisting of N integers, returns index of any element of array A in which the dominator of A occurs. The function should return −1 if array A does not have a dominator.

**Assume that:**

* N is an integer within the range [0..100,000];
* each element of array A is an integer within the range [−2,147,483,648..2,147,483,647].

For example, given array A such that

```
A[0] = 3 
A[1] = 4 
A[2] = 3 
A[3] = 2 
A[4] = 3 
A[5] = -1 
A[6] = 3 
A[7] = 3
```

the function may return 0, 2, 4, 6 or 7, as explained above.

**Complexity:**

* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(1), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

* C++1
```
int solution(vector<int> &A) {
    int leader = -1, count=0;
    for(int a : A)
    {
        if(count==0)
        {
            leader = a;
            count++;
        }
        else if(leader == a) count++;
        else count--;
    }
    count = 0;
    for(int a : A)
        if(a == leader) count++;
    if(count <= (int)A.size()/2) return -1;
    
    int res = 0;
    while(A[res]!=leader) res++;
    return res;
}
```

## Explanation

Using Moore Voting algorithm to find the most appeared element, count the number of the most appeared element

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)

## Testcase

small_nondominator  all different and all the same elements

small_half_positions  half elements the same, and half + 1 elements the same

small  small test

small_pyramid  decreasing and plateau, small

extreme_empty_and_single_item  empty and single element arrays

extreme_half1  array with exactly N/2 values 1, N even + [0,0,1,1,1]

extreme_half2  array with exactly floor(N/2) values 1, N odd + [0,0,1,1,1]

extreme_half3  array with exactly ceil(N/2) values 1 + [0,0,1,1,1]
