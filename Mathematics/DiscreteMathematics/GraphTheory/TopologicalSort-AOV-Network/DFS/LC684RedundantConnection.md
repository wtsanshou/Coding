# LC684. Redundant Connection

### LeetCode

## Question

In this problem, a tree is an undirected graph that is connected and has no cycles.

The given input is a graph that started as a tree with N nodes (with distinct values 1, 2, ..., N), with one additional edge added. The added edge has two different vertices chosen from 1 to N, and was not an edge that already existed.

The resulting graph is given as a 2D-array of edges. Each element of edges is a pair [u, v] with u < v, that represents an undirected edge connecting nodes u and v.

Return an edge that can be removed so that the resulting graph is a tree of N nodes. If there are multiple answers, return the answer that occurs last in the given 2D-array. The answer edge [u, v] should be in the same format, with u < v.

**Example 1:**
```
Input: [[1,2], [1,3], [2,3]]
Output: [2,3]
```

**Explanation:**

The given undirected graph will be like this:
```
  1
 / \
2 - 3
```

**Example 2:**
```
Input: [[1,2], [2,3], [3,4], [1,4], [1,5]]
Output: [1,4]
```

**Explanation:**

The given undirected graph will be like this:
```
5 - 1 - 2
    |   |
    4 - 3
```

**Note:**

* The size of the input 2D-array will be between 3 and 1000.
* Every integer represented in the 2D-array will be between 1 and N, where N is the size of the input array.

**Update (2017-09-26):**
We have overhauled the problem description + test cases and specified clearly the graph is an undirected graph. For the directed graph follow up please see Redundant Connection II). We apologize for any inconvenience caused.

## Solution

* Java1 (Time Limit Exceeded)

```
class Solution {
    public int[] findRedundantConnection(int[][] edges) {
        int[] res = new int[2];
        int n = edges.length;
        boolean[][] graph = new boolean[n+1][n+1];
        for(int[] edge : edges){
            boolean[][] visit = new boolean[n+1][n+1];
            if(isCircle(edge[0], edge[1], graph, visit))
                res = edge;
            graph[edge[0]][edge[1]] = true;
            graph[edge[1]][edge[0]] = true;
        }
        return res;
    }
    
    private boolean isCircle(int start, int end, boolean[][] graph, boolean[][] visit){
        if(start == end) return true;
        if(visit[start][end]) return false;
        visit[start][end] = true;
        visit[end][start] = true;
        for(int i=1; i<graph.length; ++i){
            if(graph[end][i] && isCircle(start, i, graph, visit))
                return true;
        }
        return false;
    }
}
```

* Java2 (Time Limit Exceeded)

```
class Solution {
    public int[] findRedundantConnection(int[][] edges) {
        int[] res = new int[2];
        int n = edges.length;
        Map<Integer, List<Integer>> graph = new HashMap<>();
        for(int[] edge : edges){
            boolean[][] visit = new boolean[n+1][n+1];
            if(isCircle(edge[0], edge[1], graph, visit))
                res = edge;
            if(!graph.containsKey(edge[0])) graph.put(edge[0], new ArrayList<Integer>());
            if(!graph.containsKey(edge[1])) graph.put(edge[1], new ArrayList<Integer>());
            graph.get(edge[0]).add(edge[1]);
            graph.get(edge[1]).add(edge[0]);
        }
        return res;
    }
    
    private boolean isCircle(int start, int end, Map<Integer, List<Integer>> graph, boolean[][] visit){
        if(start == end) return true;
        if(visit[start][end] || !graph.containsKey(end)) return false;
        visit[start][end] = true;
        visit[end][start] = true;
        for(int next : graph.get(end)){
            if(isCircle(start, next, graph, visit))
                return true;
        }
        return false;
    }
}
```

* Java3

```
class Solution {
    public int[] findRedundantConnection(int[][] edges) {
        int[] res = new int[2];
        int n = edges.length;
        Map<Integer, List<Integer>> graph = new HashMap<>();
        for(int[] edge : edges){
            boolean[] visit = new boolean[n+1];
            if(isCircle(edge[0], edge[1], graph, visit))
                res = edge;
            if(!graph.containsKey(edge[0])) graph.put(edge[0], new ArrayList<Integer>());
            if(!graph.containsKey(edge[1])) graph.put(edge[1], new ArrayList<Integer>());
            graph.get(edge[0]).add(edge[1]);
            graph.get(edge[1]).add(edge[0]);
        }
        return res;
    }
    
    private boolean isCircle(int start, int end, Map<Integer, List<Integer>> graph, boolean[] visit){
        if(start == end) return true;
        if(visit[end] || !graph.containsKey(end)) return false;
        visit[end] = true;
        for(int next : graph.get(end)){
            if(isCircle(start, next, graph, visit))
                return true;
        }
        return false;
    }
}
```

## Explanation

Using DFS to find a circle in the graph.

**Java1** using 2D array to create the graph, but check too much empty edge.

**Java2** using hash map to create the graph, but check too much visit.

**Java3** Only check the end vertice visiting is enough.

Another solution: <a href="https://en.wikipedia.org/wiki/Disjoint-set_data_structure">Disjoint Set Union (DSU)</a> data structure.

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(n)