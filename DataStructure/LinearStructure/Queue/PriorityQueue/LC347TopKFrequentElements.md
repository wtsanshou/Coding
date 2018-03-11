# LC347. Top K Frequent Elements

### LeetCode

## Question

Given a non-empty array of integers, return the k most frequent elements.

**For example,**
```
Given [1,1,1,2,2,3] and k = 2, return [1,2].
```

**Note:** 

* You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
* Your algorithm's time complexity must be better than O(n log n), where n is the array's size.

## Solutions

* C++1 (19ms)
```
vector<int> topKFrequent(vector<int>& nums, int k) {
    unordered_map<int, int> count;
    for(auto num : nums)
        count[num]++;
    priority_queue<int, vector<int>, greater<int>> pq;
    for(auto ele : count)
    {
        pq.push(ele.second);
        if(pq.size()>k) pq.pop();
    }
    vector<int>res;
    for(auto ele : count)
        if(ele.second >= pq.top())
            res.push_back(ele.first);
    return res;
}
```

* C++2 
```
vector<int> topKFrequent(vector<int>& nums, int k) {
    unordered_map<int, int> counts;
    for(int n : nums) ++counts[n];
    vector<vector<int>> buckets(nums.size()+1); // no 0 frequent elements
    for(auto m : counts)
    {
        buckets[m.second].push_back(m.first);
    }
    vector<int> res;
    for(int i=buckets.size()-1; i>=0; --i)
    {
        for(int j=0; j<buckets[i].size(); ++j)
        {
            res.push_back(buckets[i][j]);
            if(res.size()>=k) return res;
        }
    }
    return res;
}
```

* Java1
```
public List<Integer> topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> freqMap = new HashMap<>();
    PriorityQueue<Map.Entry<Integer, Integer>> pq = 
                                        new PriorityQueue<>((a, b) -> a.getValue() - b.getValue());
    List<Integer> res = new ArrayList<>();
    
    for(int num : nums)
    {
        int count = freqMap.getOrDefault(num, 0);
        freqMap.put(num, count + 1);
    }
    
    for(Map.Entry<Integer, Integer> map : freqMap.entrySet())
    {
        pq.offer(map);
        if(pq.size()>k)
            pq.poll();
    }
    
    while(!pq.isEmpty())
    {
        int num = pq.poll().getKey();
        res.add(num);
    }
    return res;
}
```

* Java2
```
public List<Integer> topKFrequent(int[] nums, int k) {
        int len = nums.length;
        Map<Integer, Integer> freqMap = new HashMap<>();
        List<Integer> [] buckets = new List[len+1];
        List<Integer> res = new ArrayList<>();
        
        for(int num : nums)
        {
            freqMap.put(num, freqMap.getOrDefault(num, 0) + 1);
        }
        
        for(int key : freqMap.keySet())
        {
            int freq = freqMap.get(key);
            if(buckets[freq] == null)
            {
                buckets[freq] = new ArrayList();
            }
            buckets[freq].add(key);
        }
/*
for(Map.Entry<Integer, Integer> map : freqMap.entrySet())
        {
            int freq = map.getValue();
            if(buckets[freq] == null)
            {
                buckets[freq] = new ArrayList();
            }
            buckets[freq].add(map.getKey());
        }
*/
        
        for(int i=len; i>0; --i)
        {
            if(buckets[i]==null) continue;
            for(int j=0; j<buckets[i].size(); ++j)
            {
                res.add(buckets[i].get(j));
                if(res.size()>= k) 
                    return res;
            }
        }
        return res;
}
```

## Explanation

The most straight forward idea is to count the frequencies of the input numbers and sort it by their frequencies. But the algorithm's time complexity would be  `O(Nlog(N))`. It does not meet the condition of the question.

A O(n) sorting algorithm is bucket sort. So,

**Solution 1**

1. Count the frequencies of the input numbers. (`O(N)`)
2. Create buckets with the frequencies as indexes.
3. Put the input numbers into these buckets.
4. Traverse these buckets from higher indexes to lower indexes, get the top `k` most frequent elements.

**Solution 2**

Using a <a href="https://en.wikipedia.org/wiki/Priority_queue">Priority Queue</a> with the frequencies as priority, we can keep the size of the queue in `k` elements (Save a little bit space than the buckets algorithm). After insert (`O(log(N))`) all elements of the counted numbers, the queue will only contain the top `k` most frequent elements.

* **worst-case time complexity:** `O(N)`, where `N` is the array's size.
* **worst-case space complexity:** `O(N)`, where `N` is the array's size.


