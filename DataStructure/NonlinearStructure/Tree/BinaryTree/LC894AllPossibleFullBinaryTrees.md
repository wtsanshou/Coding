# LC894. All Possible Full Binary Trees

### LeetCode

## Question

A full binary tree is a binary tree where each node has exactly 0 or 2 children.

Return a list of all possible full binary trees with N nodes.  Each element of the answer is the root node of one possible tree.

Each node of each tree in the answer must have node.val = 0.

You may return the final list of trees in any order.

**Example 1:**
```
Input: 7
Output: [[0,0,0,null,null,0,0,null,null,0,0],[0,0,0,null,null,0,0,0,0],[0,0,0,0,0,0,0],[0,0,0,0,0,null,null,null,null,0,0],[0,0,0,0,0,null,null,0,0]]
Explanation:
```
 
![LC894. All Possible Full Binary Trees](Images/LC894AllPossibleFullBinaryTrees.png)

**Note:**

* 1 <= N <= 20

## Solutions

* Java1
```
class Solution {

    private static Map<Integer, List<TreeNode>> res = new HashMap();
    
    public List<TreeNode> allPossibleFBT(int N) {
        if(!res.containsKey(N)){
            List<TreeNode> ans = new ArrayList();
            if(N == 1){
                ans.add(new TreeNode(0));
            }else if(N % 2 == 1){
                for(int x=0; x<N; ++x){
                    int y = N-1-x;
                    for(TreeNode left : allPossibleFBT(x))
                        for(TreeNode right : allPossibleFBT(y)){
                            TreeNode root = new TreeNode(0);
                            root.left = left;
                            root.right = right;
                            ans.add(root);
                        }
                }
            }
            res.put(N, ans);
        }
        return res.get(N);
    }
}
```

* Scala1
```
object Solution {
    
    var res = new scala.collection.mutable.HashMap[Integer, List[TreeNode]]() 
    
    def allPossibleFBT(N: Int): List[TreeNode] = {
        if(!Solution.res.contains(N)){
            var ans = List[TreeNode]()
            if(N==1){
                ans = ans :+ new TreeNode(0)
            }else if(N%2 == 1){
                for(x <- 0 until N){
                    val y = N-1-x
                    for(left  <- allPossibleFBT(x);
                        right <- allPossibleFBT(y)){
                        var root = new TreeNode(0)
                        root.left = left
                        root.right = right
                        ans = ans :+ root
                    }
                }
            }
            Solution.res.put(N, ans)
        }
        Solution.res.get(N).head
    }
}
```

## Explanation

Using static variable could remove the duplicated calculation of `allPossibleFBT(x)` and `allPossibleFBT(y)`.

* **worst-case time complexity:** `O(2<sup>N</sup>)`.
* **worst-case space complexity:** `O(2<sup>N</sup>)`.
