# LC621. Task Scheduler

### LeetCode

## Question

Given a char array representing tasks CPU need to do. It contains capital letters `A` to `Z` where different letters represent different tasks.Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the least number of intervals the CPU will take to finish all the given tasks.

**Example 1:**

```
Input: tasks = ['A','A','A','B','B','B'], n = 2
Output: 8
```

Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.

**Note:**

1.  The number of tasks is in the range [1, 10000].
2.  The integer n is in the range [0, 100].

## Solution

* C++1

```
int leastInterval(vector<char>& tasks, int n) {
        vector<int> letters(26);
        for(char c : tasks)
            letters[c-'A']++;
        sort(letters.begin(), letters.end(), greater<int>());
        int idle = letters[0]-1;
        int idleSum = idle*n;
        for(int i= 1; i<26 && letters[i]>0; ++i)
            idleSum -= min(letters[i], idle);
        return tasks.size() + ((idleSum>0) ? idleSum : 0);
}
```

* Java1

```
public int leastInterval(char[] tasks, int n) {
        int[] map = new int[26];
        for(char c : tasks)
            map[c-'A']++;
        Arrays.sort(map);
        int idle = map[25]-1;
        int idleSum = idle*n;
        for(int i=24; i>=0 && map[i]>0; --i)
            idleSum -= Math.min(map[i], idle);
        return tasks.length + ((idleSum > 0) ? idleSum : 0);
    }
```

## Explanation

* **worst-case time complexity:** O(N)
* **worst-case space complexity:** O(N)