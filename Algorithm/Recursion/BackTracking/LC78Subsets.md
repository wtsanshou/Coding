# LC78. Subsets

### LeetCode

## Question

Given a set of distinct integers, nums, return all possible subsets.

**Note:** The solution set must not contain duplicate subsets.

**For example**
```
If nums = [1,2,3], a solution is:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

## Solutions

### Solution 1

* C++ (9ms)
```
class Solution {
public:
    void backTracking(vector<vector<int>>& res, vector<int>& aRow, vector<int>& nums, int start, int end)
    {
        if(start <= end)
        {
            res.push_back(aRow);
            for(int i=start; i<end; ++i)
            {
                aRow.push_back(nums[i]);
                backTracking(res, aRow, nums, i+1, end);
                aRow.pop_back();
            }
        }
    }
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> aRow;
        backTracking(res, aRow, nums, 0, nums.size());
        return res;
    }
};
```

* Java
```
public class Solution {
    
    private List<List<Integer>> res;
    
    public List<List<Integer>> subsets(int[] nums) {
        res = new LinkedList<>();
        List<Integer> arow = new LinkedList<Integer>();
        collectSubsets(arow, nums, 0);
        return res;
    }
    
    private void collectSubsets(List<Integer> arow, int[] nums, int start){
        List<Integer> ares = new LinkedList<Integer>(arow);
        res.add(ares);
        for(int i=start; i<nums.length; ++i){
            arow.add(nums[i]);
            collectSubsets(arow, nums, i+1);
            arow.remove(arow.size()-1);
        }
    }
}
```

Typical `back tracking` algorithm.

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the length of the `nums`.
* **worst-case space complexity:** O(2<sup>n</sup>), where `n` is the length of the `nums`.

### Solution 2

* C++
```
vector<vector<int>> subsets(vector<int>& nums) {
    vector<vector<int>> res(1,vector<int>());
    for(int i=0; i<nums.size(); ++i)
    {
        int n = res.size();
        for(int j=0; j<n; ++j)
        {
            res.push_back(res[j]);
            res.back().push_back(nums[i]);
        }
    }
    return res;
}
```

* Java
```
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> firstRow = new ArrayList<Integer>();
    res.add(firstRow);
    //Arrays.sort(nums);
    for(int i=0; i<nums.length; ++i){
        int len = res.size();
        for(int j=0; j<len; ++j){
            res.add(new ArrayList<Integer>(res.get(j)));
            res.get(res.size()-1).add(nums[i]);
        }
    }
    return res;
}
```

iteration way of `back tracking`.

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the length of the `nums`.
* **worst-case space complexity:** O(2<sup>n</sup>), where `n` is the length of the `nums`.