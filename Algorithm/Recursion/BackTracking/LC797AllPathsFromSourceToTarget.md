# LC797. All Paths From Source to Target

### LeetCode

## Question

Given a directed, acyclic graph of `N` nodes.  Find all possible paths from node `0` to node `N-1`, and return them in any order.

The graph is given as follows:  the nodes are `0, 1, ..., graph.length - 1`.  `graph[i]` is a list of all nodes `j` for which the edge `(i, j)` exists.

**Example:**
```
Input: [[1,2], [3], [3], []] 
Output: [[0,1,3],[0,2,3]] 
Explanation: The graph looks like this:
0--->1
|    |
v    v
2--->3
There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```

**Note:**

* The number of nodes in the graph will be in the range [2, 15].
* You can print different paths in any order, but you should keep the order of nodes inside one path.

## Solutions

* Java1
```
class Solution {
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> aPath = new LinkedList<>();
        if(graph.length == 1 && graph[0].length == 0){
            addAPath(result, aPath, 0);
            return result;
        } 
        boolean[] visit = new boolean[graph.length];
        addPaths(result, aPath, graph, visit, 0);
        return result;
    }
    
    private void addAPath(List<List<Integer>> result, List<Integer> aPath, int node){
        aPath.add(node);
        result.add(aPath);
    }
    
    private void addPaths(List<List<Integer>> result, List<Integer> aPath, int[][] graph, boolean[] visit, int node){
        if(node == graph.length-1){
            addAPath(result, aPath, node);
            return;
        }
        if(visit[node]) return;
        visit[node] = true;
        for(int i=0; i<graph[node].length; ++i){
            List<Integer> nextPath = new ArrayList(aPath);
            nextPath.add(node);
            addPaths(result, nextPath, graph, visit, graph[node][i]);
        }
        visit[node] = false;
    }
}
```


## Explanation

Starting from node `0`, traverse the whole graph. Once found a path to the final node `N-1`, add it to the result.

**NOTE:** using a `visit` to prevent cycle in the graph.

back tracking for initial the `visit` and the `newPath`.
 
* **worst-case time complexity:** O(M*N), where M is the maximum width of the input `int[][] graph`, N is the height the input `int[][] graph`.
* **worst-case space complexity:** O(M*N), where M is the maximum width of the input `int[][] graph`, N is the height the input `int[][] graph`.