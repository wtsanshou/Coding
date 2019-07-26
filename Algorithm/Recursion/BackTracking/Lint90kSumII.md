# Lint90. k Sum II

### LintCode

## Question

Given n unique postive integers, number k (1<=k<=n) and target.

Find all possible k integers where their sum is target.

**Example 1:**
```
Input: 
[1,2,3,4], k = 2, target = 5

Output:  
[[1,4],[2,3]]
```

**Example 2:**
```
Input: 
[1,3,4,6], k = 3, target = 8

Output:  
[[1,3,4]]	
```

## Solutions

### Solution 1

* Java
```
public class Solution {
    /*
     * @param A: an integer array
     * @param k: a postive integer <= length(A)
     * @param target: an integer
     * @return: A list of lists of integer
     */
    public List<List<Integer>> kSumII(int[] A, int k, int target) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> one = new ArrayList<>();
        Arrays.sort(A);
        backTracking(A, k, target, res, one, 0);
        return res;
    }
    
    private void backTracking(int[] A, int k, int target, List<List<Integer>> res, List<Integer> one, int start) {
        if (start >= A.length || target < 0 || one.size() >= k) {
            if (target == 0 && one.size() == k) {
                res.add(new ArrayList<>(one));
            }
            return;
        }
        
        for (int i = start; i < A.length; i++) {
            if (target - A[i] < 0) break;
            one.add(A[i]);
            backTracking(A, k, target - A[i], res, one, i + 1);
            one.remove(one.size()-1);
        }
    }
}
```

At first, the question make me think of **Two Sum**, **Three Sum**, and **Four Sum**. They all need to sort the input. But for **K Sum**, It's not possible to use `k` loop to solve. 

For seeking a number of combinations, the `back tracking` came to my mind. Here sorting the input and `if (target - A[i] < 0) break;` can speed up this solution.

**NOTE** read the question carefully, the question is to find all possible **k integers**, not less than **k integers**.

**Complexity:**

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the length of the input `A`.
* **worst-case space complexity:** O(n<sup>2</sup>), where `n` is the length of the input `A`.
