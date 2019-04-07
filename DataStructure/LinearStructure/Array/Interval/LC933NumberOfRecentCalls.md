# LC933. Number of Recent Calls

### LeetCode

## Question

Write a class RecentCounter to count recent requests.

It has only one method: ping(int t), where t represents some time in milliseconds.

Return the number of pings that have been made from 3000 milliseconds ago until now.

Any ping with time in [t - 3000, t] will count, including the current ping.

It is guaranteed that every call to ping uses a strictly larger value of t than before.

**Example 1:**
```
Input: inputs = ["RecentCounter","ping","ping","ping","ping"], inputs = [[],[1],[100],[3001],[3002]]
Output: [null,1,2,3,3]
```

**Note:**

* Each test case will have at most 10000 calls to ping.
* Each test case will call ping with strictly increasing values of t.
* Each call to ping will have 1 <= t <= 10^9.

## Solutions

* Scala1 (Time Limit Exceeded, 63 / 68 test cases passed.)
```
class RecentCounter() {
    var times = List[Int]()
    
    def ping(t: Int): Int = {
        times = times :+ t
        times.size - times.indexWhere(_ >= t-3000)
    }
}
```

* Scala2 (Time Limit Exceeded, 57 / 68 test cases passed.)
```
class RecentCounter() {

    var times = List[Int]()
    
    def ping(t: Int): Int = {
        times = times :+ t
        times.size - binarySerarch(times, t-3000)
    }
    
    def binarySerarch(list: List[Int], t: Int): Int = {
        var (i, j) = (0, list.size-1)
        while( i < j){
            val mid = i + (j-i)/2
            if(list(mid) == t) return mid
            else if(list(mid) > t) j = mid
            else i = mid + 1
        }
        i
    }

}
```

* Scala3 (1384 ms)
```
class RecentCounter() {

    var times = new scala.collection.mutable.Queue[Int]
    
    def ping(t: Int): Int = {
        times += t
        while(times.head < t-3000) times.dequeue
        times.size
    }

}
```

* Scala4 (1852 ms)
```
class RecentCounter() {

    var times = Array[Int]()
    var i = 0
    def ping(t: Int): Int = {
        times = times :+ t
        while(times(i) < t-3000) i += 1
        times.size - i
    }

}
```

* Java
```
class RecentCounter {

    private Queue<Integer> queue;
    private static final int INTERVAL = 3000;
    
    public RecentCounter() {
        queue = new LinkedList<>();
    }
    
    public int ping(int t) {
        queue.offer(t);
        while(t-queue.peek() > INTERVAL)
            queue.poll();
        return queue.size();
    }
}
```

## Explanation

The first two solutions use binary Serarch. The worst-case time complexity is O(N*log(N)) which is Time Limit Exceeded.

So, we have to use queue to only keep the times within 3000 milliseconds.

* **worst-case time complexity:** O(N)
* **worst-case space complexity:** O(N)
