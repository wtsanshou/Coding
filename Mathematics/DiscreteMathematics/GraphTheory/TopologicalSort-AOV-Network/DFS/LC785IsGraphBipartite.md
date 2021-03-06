# LC785. Is Graph Bipartite?

### LeetCode

## Question

Given an undirected graph, return true if and only if it is bipartite.

Recall that a graph is bipartite if we can split it's set of nodes into two independent subsets A and B such that every edge in the graph has one node in A and another node in B.

The graph is given in the following form: `graph[i]` is a list of indexes `j` for which the edge between nodes `i` and `j` exists.  Each node is an integer between `0` and `graph.length - 1`.  There are no self edges or parallel edges: `graph[i]` does not contain `i`, and it doesn't contain any element twice.

**Example 1:**
```
Input: [[1,3], [0,2], [1,3], [0,2]]
Output: true
Explanation: 
The graph looks like this:
0----1
|    |
|    |
3----2
We can divide the vertices into two groups: {0, 2} and {1, 3}.
```

**Example 2:**
```
Input: [[1,2,3], [0,2], [0,1,3], [0,2]]
Output: false
Explanation: 
The graph looks like this:
0----1
| \  |
|  \ |
3----2
We cannot find a way to divide the set of nodes into two independent subsets.
```

**Note:**

* graph will have length in range [1, 100].
* graph[i] will contain integers in range [0, graph.length - 1].
* graph[i] will not contain i or duplicate values.
* The graph is undirected: if any element j is in graph[i], then i will be in graph[j].

## Solutions

* Java1
```
class Solution {
    public boolean isBipartite(int[][] graph) {
        Set<Integer> setA = new HashSet();
        Set<Integer> setB = new HashSet();
        for(int i=0; i<graph.length; ++i){
            if(!isPartOfBipartite(graph, i, setA, setB)) return false;
        }
        return true;
    }
    
    private boolean isPartOfBipartite(int[][] graph, int i, Set<Integer> setA, Set<Integer> setB){
        if(setA.contains(i) || setB.contains(i)) return true;
        setA.add(i);
        
        for(int ele : graph[i]){
            if(setA.contains(ele) || !isPartOfBipartite(graph, ele, setB, setA)) return false;
        }
        return true;
    }  
}
```

* Python (DFS)
```
class Solution:
    def isBipartite(self, graph: List[List[int]]) -> bool:
        n = len(graph)
        a_or_b = [0] * n
        for i in range(n):
            if a_or_b[i] == 0 and not self.valid_bipartite(i, a_or_b, 1, graph):
                return False
        return True
    
    def valid_bipartite(self, i: int, a_or_b: [], color: int, graph: List[List[int]]):
        if a_or_b[i] != 0:
            return a_or_b[i] == color
        
        a_or_b[i] = color
        for next in graph[i]:
            if not self.valid_bipartite(next, a_or_b, -color, graph):
                return False
        return True
```

* Python

```
import queue

class Solution:
    def isBipartite(self, graph: List[List[int]]) -> bool:
        n = len(graph)
        a_or_b = [0] * n
        for i in range(n):
            if a_or_b[i] == 0:
                a_or_b[i] = 1
                q = queue.Queue()
                q.put(i)
                while not q.empty():
                    node = q.get()
                    for next in graph[node]:
                        if a_or_b[next] == a_or_b[node]:
                            return False
                        if a_or_b[next] == 0:
                            a_or_b[next] = -a_or_b[node]
                            q.put(next)
        return True
```

## Explanation

Because `The graph is undirected: if any element j is in graph[i], then i will be in graph[j]`, we can use `depth first search` to traverse each independent `network`. The `graph` might contain multiple `networks`, but independent `networks` won't affect each other.

* **worst-case time complexity:** `O(M * N)`, where `M` is the width of the `graph`, `N` is the height of the `graph`.
* **worst-case space complexity:** `O(M * N)`, where `M` is the width of the `graph`, `N` is the height of the `graph`.