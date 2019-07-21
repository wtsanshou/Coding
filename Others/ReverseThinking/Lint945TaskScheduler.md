# Lint945. Task Scheduler

### LintCode

## Question

Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks.Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the least number of intervals the CPU will take to finish all the given tasks.

**Example1**
```
Input: tasks = ['A','A','A','B','B','B'], n = 2

Output: 8

Explanation:
A -> B -> idle -> A -> B -> idle -> A -> B.
```

**Example2**
```
Input: tasks = ['A','A','A','B','B','B'], n = 1

Output: 6

Explanation:
A -> B -> A -> B -> A -> B.
```

**Notice**

* The number of tasks is in the range [1, 10000].
* The integer n is in the range [0, 100].

## Solutions

### Solution 1

* Java
```
public int leastInterval(char[] tasks, int n) {
    Map<Character, Integer> countTasks = new HashMap<>();
    for (char task : tasks) {
        if (!countTasks.containsKey(task)) {
            countTasks.put(task, 0);
        }
        
        countTasks.put(task, countTasks.get(task) + 1);
    }
    
    List<Integer> values = new LinkedList<>(countTasks.values());
    Collections.sort(values, (a, b) -> Integer.compare(b, a));
    
    int sum_task = values.stream().mapToInt(Integer::intValue).sum();
    int maxTask = values.get(0) - 1;
    int slot = maxTask * n;

    for (int i = 1; i < values.size() && slot > 0; i++)
        slot -= Math.min(values.get(i), maxTask); // the number of taks with maximum size could be more than 1
    
    return sum_task + Math.max(0, slot);
}
```

At the beginning, I can reach the step to get the sorted list of `values`. I was thinking assign tasks round by round and removed the finished tasks from the `values`. 

It takes me a lot of time to figure out how to remove elements from `map` or `list` without affect the iteration of the collections. For `Map`, you have to use iterator. An example here:

```
Iterator<Character> iterator = countTasks.keySet().iterator();
        
while(iterator.hasNext()){
  Character key = iterator.next();
  countTasks.put(key, countTasks.get(key) - 1);
  if(countTasks.get(key) <= 0){
    iterator.remove();
  }
}
```

For list, when you remove an element from the list, the index after the element will be changed. It's better to use filter to create a new list.

But for this method, after a round of task assignment, I have to sort the rest of tasks again. And the result is wrong.

The correct solution is reverse thinking. Instead of assign the tasks round by round, we notice that only the most frequent task affect the number of idle. So we can first calculate the maximum number (maxTask * n) of idle needed by the most frequent task. **Note** here `maxTask = values.get(0) - 1`, the last task does not need idle. 

Then, we can use other tasks to fill in these idle. **Note** there could be more than one most frequent tasks. So `slot -= Math.min(values.get(i), maxTask)`.

Finally, there two situations:

1. If `slot <= 0`, it means there are enough tasks to fill into the idle of the most frequent task. The least number of intervals the CPU will take to finish all the given tasks is just the total number of all tasks.
2. If `slot > 0`, it means there is not enough tasks to fill into the idle slots of the most frequent task. The least number of intervals the CPU will take to finish all the given tasks is the total number of all tasks plus the number of idle slots.

**Complexity:**

* **worst-case time complexity:** O(N * log(N)), where `N` is the length of the input `tasks`.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the input `tasks`.  
