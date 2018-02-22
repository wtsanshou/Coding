# LC729. My Calendar I

### LeetCode

## Solution

Implement a `MyCalendar` class to store your events. A new event can be added if adding the event will not cause a double booking.

Your class will have the method, `book(int start, int end)`. Formally, this represents a booking on the half open interval `[start, end)`, the range of real numbers `x` such that `start <= x < end`.

A double booking happens when two events have some non-empty intersection (ie., there is some time that is common to both events.)

For each call to the method `MyCalendar.book`, return `true` if the event can be added to the calendar successfully without causing a double booking. Otherwise, return `false` and do not add the event to the calendar.

Your class will be called like this: `MyCalendar cal = new MyCalendar(); MyCalendar.book(start, end)`

**Example 1:**
```
MyCalendar();
MyCalendar.book(10, 20); // returns true
MyCalendar.book(15, 25); // returns false
MyCalendar.book(20, 30); // returns true
```

**Explanation:**

The `first event` can be booked.  The second can't because time `15` is already booked by another event.

The `third event` can be booked, as the `first event` takes every time less than `20`, but not including `20`.

**Note:**

* The number of calls to `MyCalendar.book` per test case will be at most `1000`.
* In calls to `MyCalendar.book(start, end)`, `start` and `end` are integers in the range `[0, 10^9]`.

## Solutions

* Java1

```
class MyCalendar {

    private TreeMap<Integer, Integer> calender;
    
    public MyCalendar() {
        calender = new TreeMap<>();
    }
    
    public boolean book(int start, int end) {
        if(calender.containsKey(start)) return false;
        Integer lowerStart = calender.lowerKey(start);
        if(lowerStart != null && calender.get(lowerStart) > start) 
            return false;
        Integer higherStart = calender.higherKey(start);
        if(higherStart != null && higherStart < end) 
            return false;
        calender.put(start, end);
        return true;
    }
}
```

* Java2
```
class MyCalendar {

    private TreeMap<Integer, Integer> calender;
    
    public MyCalendar() {
        calender = new TreeMap<>();
    }
    
    public boolean book(int start, int end) {
        Integer lowerStart = calender.floorKey(start);
        if(lowerStart != null && calender.get(lowerStart) > start) 
            return false;
        Integer higherStart = calender.ceilingKey(start);
        if(higherStart != null && higherStart < end) 
            return false;
        calender.put(start, end);
        return true;
    }
}
```

## Explanation

If we maintained the booked events in sorted order by the `start`, we can find a proper place for an event in `O(log(N))` (where `N` is the size of the booked events) by binary search. Then we can check whether the event could be booked. 

If the event is addable, we should add the event into the booked events.

We need a data strcuture that keeps the booked events in sorted order and support fast insertion. In Java, `TreeMap` is the perfect candidate.

For Java, we will have a `TreeMap` where we can put the booked events' interval `(start, end)` in. Here we set `start` as `Key` and `end` as `Value`. 

**For example:**

```
booked events:     a      b    c         d 
                   -------     ----------

Add event:                x      y
                           ------
```

When we try to insert an event `(x, y)`, we check if there is a conflict on each neighbour intervals: any `x < b` or `y > c` are invalid for booking.

**Note:** 

1. If `(a, b)` or `(c, d)` is null, there is no conflict on each side respectively.
2. `TreeMap.higherKey` and `TreeMap.lowerKey` do not return the target key itself. You can use `TreeMap.ceilingKey` and `TreeMap.floorKey` instead.

* **worst-case time complexity:** O(Nlog(N))
* **worst-case space complexity:** O(N)