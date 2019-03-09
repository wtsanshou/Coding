# LC46. Permutations

### Question

Given a collection of distinct numbers, return all possible permutations.

**For example**
```
[1,2,3] have the following permutations:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

## Solutions

### Solution 1

* C++1 (13ms)
```
class Solution {
public:
    void permutaion(vector<vector<int>>& res, vector<int>& aRow, vector<int>& nums, int start)
    {
        if(start == nums.size()) res.push_back(aRow);
        else
        {
            for(int i=start; i<nums.size(); ++i)
            {
                swap(nums[start], nums[i]);
                aRow.push_back(nums[start]);

                permutaion(res, aRow, nums, start+1);

                swap(nums[start], nums[i]);
                aRow.pop_back();
            }
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> aRow;

        permutaion(res, aRow, nums, 0);

        return res;
    }
};
```

* C++2 (16ms)
```
class Solution {
public:
    void permuteHelper(vector<vector<int>>& res, vector<int>& aRow, vector<int>& nums)
    {
        if(aRow.size() == nums.size())
            res.push_back(aRow);
        else
        {
            for(int i=0; i<nums.size(); ++i)
            {
                if(find(aRow.begin(), aRow.end(), nums[i]) == aRow.end())
                {
                    aRow.push_back(nums[i]);
                    permuteHelper(res, aRow, nums);
                    aRow.pop_back();
                }
            }
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> aRow;

        permuteHelper(res, aRow, nums);

        return res;
    }
};
```

* C++3 
```
class Solution {
public:
    void permutaion(vector<vector<int>>& res,vector<int>& nums, int start)
    {
        if(start == nums.size()) res.push_back(nums);
        else
        {
            for(int i=start; i<nums.size(); ++i)
            {
                swap(nums[start], nums[i]);
                permutaion(res, nums, start+1);
                swap(nums[start], nums[i]);
            }
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> res;

        permutaion(res, nums, 0);

        return res;
    }
};
```

* Java1 (6ms)
```
public class Solution {
    private List<List<Integer>> res;
    
    public List<List<Integer>> permute(int[] nums) {
        res = new ArrayList<>();
        List<Integer> arow = new LinkedList<Integer>();

        createPermute(arow, nums, 0);

        return res;
    }
    
    private void createPermute(List<Integer> arow, int[] nums, int start)
    {
        if(arow.size() == nums.length)
        {
            List<Integer> ans = new LinkedList<Integer>(arow);
            res.add(ans);
            return;
        }

        for(int i=start; i<nums.length; ++i)
        {
            mySwap(nums, start, i);
            arow.add(nums[start]);

            createPermute(arow, nums, start+1);

            mySwap(nums, start, i);
            arow.remove(arow.size()-1);
        }
    }
    
    private void mySwap(int[] nums, int i, int j)
    {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

#### Explanation

Using `back tracking` algorithm.

* **worst-case time complexity:** O(N<sup>2</sup>), where `N` is the length of the input `nums`.
* **worst-case space complexity:** O(N<sup>2</sup>), where `N` is the length of the input `nums`.