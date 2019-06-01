# LC508. Most Frequent Subtree Sum

### LeetCode

## Question

Given the root of a tree, you are asked to find the most frequent subtree sum. The subtree sum of a node is defined as the sum of all the node values formed by the subtree rooted at that node (including the node itself). So what is the most frequent subtree sum value? If there is a tie, return all the values with the highest frequency in any order.

**Examples 1**
```
Input:
  5
 /  \
2   -3
return [2, -3, 4], since all the values happen only once, return all of them in any order.
```

**Examples 2**
```
Input:
  5
 /  \
2   -5
return [2], since 2 happens twice, however -5 only occur once.
```

## Solutions

### Solution 1

* C++ (16ms)
```
class Solution {
public:
    int CountMaxFreq(TreeNode* root, unordered_map<int, int>& count, int& sum)
    {
        if(root==NULL)  return 0;
        int maxL = CountMaxFreq(root->left, count, sum);
        int sumR = 0;
        int maxR = CountMaxFreq(root->right, count, sumR);
        sum += root->val + sumR;
        count[sum]++;
        return max(count[sum], max(maxL, maxR));
    }
    vector<int> findFrequentTreeSum(TreeNode* root) {
        unordered_map<int, int> count;
        vector<int> res;
        int sum = 0;
        int mostFreq = CountMaxFreq(root, count, sum);
        for(pair<int, int> c : count)
            if(c.second == mostFreq) res.push_back(c.first);
        return res;
    }
};
```

Using a map to count the frequency of all subtree sum. Post-order

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.