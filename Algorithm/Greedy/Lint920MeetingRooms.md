# Lint920. Meeting Rooms

Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

**Example1**
```
Input: intervals = [(0,30),(5,10),(15,20)]
Output: false

Explanation: 
(0,30), (5,10) and (0,30),(15,20) will conflict
```

**Example2**
```
Input: intervals = [(5,8),(9,15)]
Output: true

Explanation: 
Two times will not conflict 
```

## Solutions

### Solution 1

* Java
```
public boolean canAttendMeetings(List<Interval> intervals) {
    Collections.sort(intervals, (a, b) -> Integer.compare(a.start, b.start));
    for(int i=0; i<intervals.size()-1; i++){
        if(intervals.get(i+1).start < intervals.get(i).end)
            return false;
    }
    return true;
}
```

The first greedy algorithm I had learned from the book `Introduction to Algorithms`. The key is to sort the `intervals` by the `start` time.

**Complexity:**

* **worst-case time complexity:** `O(n * log(n))`, where `n` is the length of the `intervals`.
* **worst-case space complexity:** `O(log(n))`, where `n` is the length of the `intervals`.
