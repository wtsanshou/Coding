# LC646. Maximum Length of Pair Chain

### LeetCode

## Question

You are given n pairs of numbers. In every pair, the first number is always smaller than the second number.

Now, we define a pair (c, d) can follow another pair (a, b) if and only if b < c. Chain of pairs can be formed in this fashion.

Given a set of pairs, find the length longest chain which can be formed. You needn't use up all the given pairs. You can select pairs in any order.

Example 1:

Input: [[1,2], [2,3], [3,4]]
Output: 2
Explanation: The longest chain is [1,2] -> [3,4]

Note:

1.  The number of given pairs will be in the range [1, 1000].

## Solutions

* C++1
```
int findLongestChain(vector<vector<int>>& pairs) {
        sort(pairs.begin(), pairs.end(), [](vector<int> a, vector<int> b) {
            return a[1]<b[1];
        });
        
        int res = 0, right = INT_MIN;
        for(vector<int> pair : pairs)
        {
            if(pair[0] > right)
            {
                res++;
                right = pair[1];
            }
        }
        return res;
}
```

* C++2
```
static bool myfunction (vector<int> a, vector<int> b) { return a[1]<b[1]; }
    
    int findLongestChain(vector<vector<int>>& pairs) {
        sort(pairs.begin(), pairs.end(), myfunction);
        
        int res = 0, right = INT_MIN;
        for(vector<int> pair : pairs)
        {
            if(pair[0] > right)
            {
                res++;
                right = pair[1];
            }
        }
        return res;
    }
```

*C++3
```
struct myclass {
      bool operator() (vector<int> a, vector<int> b) { return a[1]<b[1]; }
    } myobject;
    
    int findLongestChain(vector<vector<int>>& pairs) {
        sort(pairs.begin(), pairs.end(), myobject);
        
        int res = 0, right = INT_MIN;
        for(vector<int> pair : pairs)
        {
            if(pair[0] > right)
            {
                res++;
                right = pair[1];
            }
        }
        return res;
    }
```

* Java1
```
public int findLongestChain(int[][] pairs) {
        Arrays.sort(pairs, (int[] a, int[] b) -> a[1] - b[1] );
        
        int res = 0, right = Integer.MIN_VALUE;
        for(int i=0; i<pairs.length; ++i){
            if(pairs[i][0] > right){
                res++;
                right = pairs[i][1];
            }
        }
        return res;
    }
```

* Java2
```
public class Solution {
    public int findLongestChain(int[][] pairs) {
        Arrays.sort(pairs, new SortbyRight());
        
        int res = 0, right = Integer.MIN_VALUE;
        for(int i=0; i<pairs.length; ++i){
            if(pairs[i][0] > right){
                res++;
                right = pairs[i][1];
            }
        }
        return res;
    }
}

class SortbyRight implements Comparator<int[]>
{
    // Used for sorting in ascending order of right edge
    public int compare(int[] a, int[] b)
    {
        return a[1] - b[1];
    }
}
```

## Explanation

**NOTE:** The number of given pairs will be in the range [1, 1000]. The number is not the value in the pairs!

It's a typical greedy algorithm.

* **worst-case time complexity:** O(nlog(n))
* **worst-case space complexity:** O(n)