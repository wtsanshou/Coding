# LC539. Minimum Time Difference

### Question

Given a list of 24-hour clock time points in "Hour:Minutes" format, find the minimum minutes difference between any two time points in the list.

Example 1:

Input: ["23:59","00:00"]
Output: 1

Note:

1.	The number of time points in the given list is at least 2 and won't exceed 20000.
2.	The input time is legal and ranges from 00:00 to 23:59.

## Solutions

### Solution 1

* Java (46ms,  39MB)
```
class Solution {
    public int findMinDifference(List<String> timePoints) {
        int n = timePoints.size();
        List<Integer> sortedTimes = timePoints.stream()
            .map(time -> getMinutes(time))
            .sorted()
            .collect(Collectors.toList());
        int minDiff = corssDiffBetween(sortedTimes.get(0), sortedTimes.get(n-1));
        for(int i=0; i<n-1; i++)
            minDiff = Math.min(minDiff, diffBetween(sortedTimes.get(i), sortedTimes.get(i+1)));
        return minDiff;
    }
    
    private int getMinutes(String time){
        int i = time.indexOf(':');
        int hour = Integer.valueOf(time.substring(0, i));
        int minute = Integer.valueOf(time.substring(i+1));
        return hour*60 + minute;
    }
    
    private int corssDiffBetween(int t1, int t2){
        return t1 + (1440 - t2);
    }
    
    private int diffBetween(int t1, int t2){
        return t2 - t1;
    }
}
```

**Note:** This is a 24-hour clock not the 12-hour.

The idea is to sort the `timePoints` first. Then comare all the adjacent `timePoint` in the list to find out the minimum minutes difference. 

The only corner case is the two `timePoints` around `24:00`, aka the `first timePoint` and the `last timePoint`.

* **worst-case time complexity:** `O(n*log(n))`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `nums`.

### Solution 2

* C++ (13 ms)
```
class Solution {
public:
    int getTime(string timePoint)
    {
        int i=0;
        while(timePoint[i]!=':') i++;
        int hour = stoi(timePoint.substr(0,i));
        int mins = stoi(timePoint.substr(i+1));
        return 60*hour + mins;
    }
    int findMinDifference(vector<string>& timePoints) {
        int n = timePoints.size();
        int gap = 1440;
        if(n>gap) return 0;
        vector<int> minutes(gap);
        for(auto tp : timePoints)
        {
            int t = getTime(tp);
            if(minutes[t] > 0) return 0;
            minutes[t] = 1;
        }
        int start = 0;
        while(minutes[start] == 0) start++;
        int res = gap;
        for(int i=start+1; start<gap; ++i)
        {
            int next = i%gap;
            if(minutes[next] != 0)
            {
                res = min(res, (next - start + gap)%gap);
                start = i;
            }
        }
        return res;
    }
};
```

Using time index sort the `timePoints`. Make sure cover the `first timePoint` and the `last timePoint`.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `nums`.
