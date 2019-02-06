# LC119. Pascal's Triangle II

### LeetCode

## Question

Given an index k, return the kth row of the <a href="LC118PascalsTriangle.md">Pascal's triangle</a>.

```
For example, given k = 3,
Return [1,3,3,1].
```

**Note:**
* Could you optimize your algorithm to use only O(k) extra space?

## Solutions

* C++1 (3ms) O(k)space O(k2)time
```
vector<int> getRow(int rowIndex) {
    vector<int>res(rowIndex+1, 1);
    for(int i=2; i<=rowIndex; ++i)
    {
        int pre = 1;
        for(int j=1; j<i; ++j)
        {
            res[j] += pre;
            pre = res[j] - pre;
        }
    }
    return res;
}
```

* C++2 (0ms) O(k)space O(k2)time
```
vector<int> getRow(int rowIndex) {
    vector<int> res;
    for(int i=0; i<=rowIndex; i++)
    {
        res.push_back(1);
        for(int j=i-1; j>0; j--)
            res[j] = res[j] + res[j-1];
    }
    return res;
}
```

* C++3 (3ms) O(k2)space O(k2)time
```
vector<int> getRow(int rowIndex) {
    vector<int> res(1,1);
    for(int i=0; i<rowIndex; i++)
    {
        vector<int> alayer(1,1);
        for(int j=0; j<i; j++)
            alayer.push_back(res[j] + res[j+1]);
        alayer.push_back(1);
        res.swap(alayer);
    }
    return res;
}
```

* C++4 (0ms) O(k)space O(k)time
```
vector<int> getRow(int rowIndex) {
    vector<int> res(rowIndex+1,1);
    for(int i=1; i<=(rowIndex+1)/2; i++)
    {
        res[i] = res[rowIndex-i] = (long)res[i-1]*(long)(rowIndex-i+1)/i;
    }
    return res;
}
```

* Java1 (4ms) O(k)space O(k2)time
```public List<Integer> getRow(int rowIndex) {
    List<Integer> res = new LinkedList<>();
    res.add(1);
    for(int i=0; i<rowIndex; ++i)
    {
        int pre=0; 
        for(int j=0; j<res.size(); ++j)
        {
            res.set(j, pre+res.get(j));
            pre = res.get(j)-pre;
        }
        res.add(1);
    }
    return res;
}
```

## Explanation

Get `ith` row from the `(i-1)th` row.

* **worst-case time complexity:** O(numRows<sup>2</sup>)
* **worst-case space complexity:** O(numRows<sup>2</sup>)
