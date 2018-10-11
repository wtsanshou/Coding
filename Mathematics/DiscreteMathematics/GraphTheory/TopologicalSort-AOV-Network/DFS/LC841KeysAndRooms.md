# LC841. Keys and Rooms

### LeetCode

## Question

There are N rooms and you start in room 0.  Each room has a distinct number in 0, 1, 2, ..., N-1, and each room may have some keys to access the next room. 

Formally, each room i has a list of keys rooms[i], and each key rooms[i][j] is an integer in [0, 1, ..., N-1] where N = rooms.length.  A key rooms[i][j] = v opens the room with number v.

Initially, all the rooms start locked (except for room 0). 

You can walk back and forth between rooms freely.

Return true if and only if you can enter every room.

**Example 1:**
```
Input: [[1],[2],[3],[]]
Output: true
Explanation:  
We start in room 0, and pick up key 1.
We then go to room 1, and pick up key 2.
We then go to room 2, and pick up key 3.
We then go to room 3.  Since we were able to go to every room, we return true.
```

**Example 2:**
```
Input: [[1,3],[3,0,1],[2],[0]]
Output: false
Explanation: We can't enter the room with number 2.
```

**Note:**

* 1 <= rooms.length <= 1000
* 0 <= rooms[i].length <= 1000
* The number of keys in all rooms combined is at most 3000.

## Solutions

* Java1 (BFS)
```
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        int n = rooms.size();
        boolean[] openedRooms = new boolean[n];
        Queue<Integer> queue = new LinkedList<>();
        openRoom(queue, rooms, 0, openedRooms);
        while(!queue.isEmpty()){
            int roomNum = queue.poll();
            if(openedRooms[roomNum]) continue;
            openRoom(queue, rooms, roomNum, openedRooms);
        }
        for(boolean open : openedRooms)
            if(!open) return false;
        return true;
    }
    
    private void openRoom(Queue<Integer> queue, List<List<Integer>> rooms, int roomNum, boolean[] openedRooms){
        for(int room : rooms.get(roomNum))
            queue.offer(room);
        openedRooms[roomNum] = true;
    }
}
```

* Java2 (DFS)
```
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        boolean[] openedRooms = new boolean[rooms.size()];
        DFS(rooms, 0, openedRooms);
        for(boolean open : openedRooms)
            if(!open) return false;
        return true;
    }
    
    private void DFS(List<List<Integer>> rooms, int roomNum, boolean[] openedRooms){
        if(openedRooms[roomNum]) return;
        openedRooms[roomNum] = true;
        for(int room: rooms.get(roomNum))
            DFS(rooms, room, openedRooms);
    }
}
```

* Java3 (DFS)
```
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        Set<Integer> openedRooms = new HashSet<>();
        DFS(rooms, 0, openedRooms);
        return openedRooms.size() == rooms.size();
    }
    
    private void DFS(List<List<Integer>> rooms, int roomNum, Set<Integer> openedRooms){
        if(openedRooms.contains(roomNum)) return;
        openedRooms.add(roomNum);
        for(int room: rooms.get(roomNum))
            DFS(rooms, room, openedRooms);
    }
}
```

* Scala1 (DFS)
```
object Solution {
    
    var openedRooms:Set[Int] = Set();
    
    def canVisitAllRooms(rooms: List[List[Int]]): Boolean = {
        // openedRooms.empty
        DFS(rooms.toArray, 0)
        openedRooms.size == rooms.size
    }
    
    def DFS(rooms: Array[List[Int]], roomNum: Int): Unit = {
        if(openedRooms.contains(roomNum)) return
        openedRooms = openedRooms+(roomNum)
        rooms(roomNum).foreach(DFS(rooms, _))
    }
}
```

## Explanation

BFS (queue) or DFS (stack) starting from the first room. 

Using an array or set to record the visited rooms.

* **worst-case time complexity:** O(n*m), where `n` is the number of the rooms, `m` is the `rooms[i].length`.
* **worst-case space complexity:** O(n), where `n` is the number of the rooms.

