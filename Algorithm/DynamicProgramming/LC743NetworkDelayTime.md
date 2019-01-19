# LC743. Network Delay Time

### LeetCode

## Question

There are N network nodes, labelled 1 to N.

Given times, a list of travel times as directed edges times[i] = (u, v, w), where u is the source node, v is the target node, and w is the time it takes for a signal to travel from source to target.

Now, we send a signal from a certain node K. How long will it take for all nodes to receive the signal? If it is impossible, return -1.

**Note:**

* N will be in the range [1, 100].
* K will be in the range [1, N].
* The length of times will be in the range [1, 6000].
* All edges times[i] = (u, v, w) will have 1 <= u, v <= N and 1 <= w <= 100.

## Solutions

* Java1 (DFS 231ms)
```
class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        int[][] netMatrix = new int[N+1][N+1];
        for(int[] link : netMatrix)
            Arrays.fill(link, -1);
        int[] minDelay = new int[N+1];
        Arrays.fill(minDelay, -1);
        for(int[] time: times)
            netMatrix[time[0]][time[1]] = time[2];
        dfs(netMatrix, minDelay, K, 0);
        return findLatestNode(minDelay);
    }
    
    private void dfs(int[][] netMatrix, int[] minDelay, int K, int delay){
        if(minDelay[K] != -1 && minDelay[K] <= delay) return;
        minDelay[K] = delay;
        for(int i=1; i<netMatrix[K].length; ++i)
            if(netMatrix[K][i] != -1)
                dfs(netMatrix, minDelay, i, delay+netMatrix[K][i]);
    }
    
    private int findLatestNode(int[] minDelay){
        int result = -1;
        for(int i=1; i<minDelay.length; ++i){
            if(minDelay[i] == -1) return -1;
            result = Math.max(result, minDelay[i]);
        }
        return result;
    }
}
```

* Java2 (DFS + Priority Queue 179ms)
```
class Solution {
    
    private Map<Integer, PriorityQueue<int[]>> map;
    
    public int networkDelayTime(int[][] times, int N, int K) {
        map = new HashMap<>();
        for(int[] time: times){
            if(!map.containsKey(time[0]))
                map.put(time[0], new PriorityQueue<int[]>(6000, (a, b) -> a[1] - b[1]));
            map.get(time[0]).offer(new int[]{time[1], time[2]});
        }
        int[] minDelay = new int[N+1];
        Arrays.fill(minDelay, -1);
        dfs(minDelay, K, 0);
        return findLatestNode(minDelay);
    }
    
    private void dfs(int[] minDelay, int K, int delay){
        if(minDelay[K] != -1 && minDelay[K] <= delay) return;
        minDelay[K] = delay;
        if(!map.containsKey(K)) return;  // Could be no K in the map here
        for(int[] nextNode : this.map.get(K))
            dfs(minDelay, nextNode[0], delay+nextNode[1]);
    }
    
    private int findLatestNode(int[] minDelay){
        int result = -1;
        for(int i=1; i<minDelay.length; ++i){
            if(minDelay[i] == -1) return -1;
            result = Math.max(result, minDelay[i]);
        }
        return result;
    }
}
```

* Java3 (DP 68ms)
```
class Solution {
    
    public int networkDelayTime(int[][] times, int N, int K) {
        int[] minDelay = new int[N+1];
        Arrays.fill(minDelay, 600001);  // The sum of all delay should be less than this number 600001.
        minDelay[K] = 0;
        for(int i=1; i<N; ++i) // N-1 times is the maximum times to fill all minDelay.
            for(int[] link : times)
                minDelay[link[1]] = Math.min(minDelay[link[1]], minDelay[link[0]] + link[2]);
        return findLatestNode(minDelay);
    }
    
    private int findLatestNode(int[] minDelay){
        int result = -1;
        for(int i=1; i<minDelay.length; ++i){
            if(minDelay[i] == 600001) return -1;
            result = Math.max(result, minDelay[i]);
        }
        return result;
    }
}
```

## Explanation

DFS search start from `K`.

DFS + Priority Queue will reduce some DFS

DP check the `times` `N-1` times to make sure all minDelay are filled.

* **worst-case time complexity:** `O(M*N)`, where `M` is the length of `times`.
* **worst-case space complexity:** O(N).
