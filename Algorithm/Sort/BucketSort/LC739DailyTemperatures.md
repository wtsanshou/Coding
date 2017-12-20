# LC739. Daily Temperatures

### LeetCode

## Question

Given a list of daily temperatures, produce a list that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.

For example, given the list temperatures = [73, 74, 75, 71, 69, 72, 76, 73], your output should be [1, 1, 4, 2, 1, 1, 0, 0].

Note: The length of temperatures will be in the range [1, 30000]. Each temperature will be an integer in the range [30, 100].

## Solutions

* C#1
```
public int[] DailyTemperatures(int[] temperatures) {
    int n = temperatures.Length;
    List<int>[] lists = new List<int>[101];
    for(int i=0; i<n; ++i){
        if(lists[temperatures[i]] == null)
            lists[temperatures[i]] = new List<int>();
        lists[temperatures[i]].Add(i);
    }
    int[] res = new int[n];
    for(int i=0; i<n; ++i){
        int min = 30001;
        for(int t = temperatures[i]+1; t<=100; ++t){
            if(lists[t] != null){
                while(lists[t].Count != 0 && lists[t][0] < i)
                    lists[t].RemoveAt(0);
                if(lists[t].Count != 0)
                    min = Math.Min(min, lists[t][0]-i);
            }
        }
        if(min != 30001) res[i] = min;
    }
    return res;
}
```

## Explanation

1. Bucket sort the temperatures.
2. For each temperature, compare the first future locations of all warmer temperature buckets. While remove all temperatures which are located before the current temperatures, because they would not be considered in the future.
3. The closest location is the required waiting days.

**Corner cases:**

1. No wamer temperatures than the current temperatures.
2. All wamer temperatures are located before the current temperatures.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)
