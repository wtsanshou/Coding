# LC118. Pascal's Triangle

### LeetCode

## Question

Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,

Return

```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

## Solutions

* C++1 (3ms)
```
vector<vector<int>> generate(int numRows) {
    vector<vector<int>> res(numRows, vector<int>(1, 1));
    for(int i=1; i<numRows; ++i)
    {
        for(int j=0; j<res[i-1].size(); ++j)
        {
            if(j==res[i-1].size()-1) res[i].push_back(res[i-1][j]);
            else res[i].push_back(res[i-1][j] + res[i-1][j+1]);
        }
    }
    return res;
}
```

* C++2 (0ms)
```
vector<vector<int>> generate(int numRows) {
    vector<vector<int>> res;
    if(numRows<1) return res;
    vector<int> lastRow(1,1);
    res.push_back(lastRow);
    for(int i=1; i<numRows; i++)
    {
        vector<int> aRow(1,1);
        for(int j=0; j<i-1;j++)
            aRow.push_back(lastRow[j] + lastRow[j+1]);
        aRow.push_back(1);
        lastRow.swap(aRow);
        res.push_back(lastRow);
    }
    return res;
}
```

* Java1 (1ms)
```
public List<List<Integer>> generate(int numRows) {
    List<List<Integer>> res = new ArrayList<>();
    for(int i=0; i<numRows; ++i)
    {
        int pre=0;
        List<Integer> arow = new ArrayList<>();
        for(int j=0; i>0&&j<res.get(i-1).size(); ++j)
        {
            arow.add(pre+res.get(i-1).get(j));
            pre=res.get(i-1).get(j);
        }
        arow.add(1);
        res.add(arow);
    }
    return res;
}
```

## Explanation

Get `ith` row from the `(i-1)th` row.

* **worst-case time complexity:** O(numRows<sup>2</sup>)
* **worst-case space complexity:** O(numRows<sup>2</sup>)
