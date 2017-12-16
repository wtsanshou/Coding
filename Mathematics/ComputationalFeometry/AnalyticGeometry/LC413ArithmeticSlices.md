# LC413. Arithmetic Slices

### LeetCode

## Question

A sequence of number is called arithmetic if it consists of at least three elements and if the difference between any two consecutive elements is the same.

For example, these are arithmetic sequence:

```
1, 3, 5, 7, 9
7, 7, 7, 7
3, -1, -5, -9
```

The following sequence is not arithmetic.

```
1, 1, 2, 5, 7
```
 
A zero-indexed array A consisting of N numbers is given. A slice of that array is any pair of integers (P, Q) such that 0 <= P < Q < N.

A slice (P, Q) of array A is called arithmetic if the sequence: A[P], A[p + 1], ..., A[Q - 1], A[Q] is arithmetic. In particular, this means that P + 1 < Q.

The function should return the number of arithmetic slices in the array A.
 
**Example:**

```
A = [1, 2, 3, 4]
```

**return:**

3, for 3 arithmetic slices in A: [1, 2, 3], [2, 3, 4] and [1, 2, 3, 4] itself.

## Solutions

* C++1 (3ms) O(n)
```
int numberOfArithmeticSlices(vector<int>& A) {
    int res =0, ALen = A.size(), count=0;
    vector<int> minus(ALen);
    for(int i=1; i<ALen; ++i)
        minus[i] = A[i] - A[i-1];
    for(int i=2; i<ALen; ++i)
    {
        if(minus[i] == minus[i-1])
        {
            count++;
            continue;
        }
        if(count>0)
        {
            res += (count*(count+1))/2;
            count = 0;
        }
    }
    return (count>0) ? res + (count*(count+1))/2 : res;
}
```

* Java1 (2ms) O(n)
```
public int numberOfArithmeticSlices(int[] A) {
    int ALen = A.length, res=0, count=0;
    int[] minus = new int[ALen];
    for(int i=1; i<ALen; ++i)
        minus[i] = A[i]-A[i-1];
    for(int i=2; i<ALen; ++i)
    {
        if(minus[i] == minus[i-1])
            count++;
        else if(count>0)
        {
            res += (count*(count+1))/2;
            count = 0;
        }
    }
    return count>0 ? res + count*(count+1)/2 : res;
}
```

## Explanation

The arithmetic slices need consecutive elements. So the minimum number of elements is 3. We can add element one by one, and see what happened:

```
Element number:     <3     3        4       5       6       7   ...
Slices number :     0      1        3       6       10      15  ...
Added number  :     0      1        2       3       4       5   ...
```

Therefore, the number of arithmetics slices of a consecutive elements is sum of the `Added number`. So we can use the <a href="https://en.wikipedia.org/wiki/Triangular_number">Triangular Number</a>

![Triangular Number](Images/TriangularNumber.tiff)

Then, We just need to see how many group of consecutive elements in the array.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)
