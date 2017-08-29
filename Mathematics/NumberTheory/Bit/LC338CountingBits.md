# LC338. Counting Bits

### LeetCode

## Question

Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example:

For num = 5 you should return [0,1,1,2,1,2].

Follow up:

It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?

Space complexity should be O(n).

Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.

## Solutions

* C++1 (85ms) 
```
vector<int> countBits(int num) {
    vector<int> res(1,0);
    while(num>0)
    {
        int size= res.size();
        for(int i=0; i<size && num-->0; ++i)
        {
            res.push_back(res[i]+1);
        }
    }
    return res;
}
```

* C++2 (84ms)
```
vector<int> countBits(int num) {
    vector<int> res(num+1,0);
    for(int i=1; i<=num; ++i)
    {
        res[i] = res[i&(i-1)] + 1;
    }
    return res;
}
```

* C++3 (88ms)
```
vector<int> countBits(int num) {
    vector<int> res(num+1, 0);
    if(num==0) return res;
    res[1] = 1;
    if(num==1) return res;
    int div = 1;
    for(int i=2; i<=num; ++i)
    {
        res[i] = res[i%div] + 1;
        if(i%div == 0)
            div *= 2;
    }
    return res;
}
```

* Java1 (2ms)
```
public int[] countBits(int num) {
    int[] res = new int[num+1];
    for(int i=1; i<=num; ++i)
    {
        res[i] = res[i&(i-1)] + 1;
    }
    return res;
}
```

* Java2 (3ms)
```
public int[] countBits(int num) {
    int[] res = new int[num+1];
    if(num==0) return res;
    res[1] = 1;
    if(num==0) return res;
    int div = 1;
    for(int i=2; i<=num; ++i)
    {
        res[i] = res[i%div] + 1;
        if(i%div == 0)
            div *= 2;
    }
    return res;
}
```

## Explanation

1. You should make use of what you have produced already.
2. Divide the numbers in ranges like [2-3], [4-7], [8-15] and so on. And try to generate new range from previous.
3. Or does the odd/even status of the number help you in calculating the number of 1s?

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)

