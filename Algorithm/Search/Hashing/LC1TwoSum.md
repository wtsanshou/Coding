# LC1. Two Sum

### LeetCode

## Question

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

**Example:**
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## Solutions

### Solution 1
* C++ (13ms)  O(n)
```
vector<int> twoSum(vector<int>& nums, int target) {
    vector<int>res(2,0);
    unordered_map<int, int>map;
    for(int i=0; i<nums.size(); ++i)
        map[nums[i]] = i+1;
    for(int i=0; i<nums.size(); ++i)
    {
        int ans = target - nums[i];
        if(map[ans] > 0 && map[ans]!=i+1)
        {
            res[0] = map[ans]-1;
            res[1] = i;
            return res;
        }
    }
    return res;
}
```

Using a map to map each element to their location.

Search each element and check if is the `target - element` in the map.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `nums`.

### Solution 2

* C++ (9ms) O(n)
```
vector<int> twoSum(vector<int>& nums, int target) {
   vector<int> res(2,0);  //vector<int> res(2);
   unordered_map<int, int> map;
   for(int i=0; i<nums.size(); ++i)
   {
       if(map[target-nums[i]]>0)
       {
           res[0] = map[target-nums[i]]-1;
           res[1] = i;
           return res;
       }
       map[nums[i]] = i+1;
   }
   return res;
}
```

* Java (6ms) O(n)
```
public int[] twoSum(int[] nums, int target) {
    Map<Integer,Integer> map = new HashMap<>();
    for(int i=0; i<nums.length; ++i)
    {
        int ans = target - nums[i];
        if(map.containsKey(ans))
            return new int[] {map.get(ans), i};
        else
            map.put(nums[i], i);
    }
    return new int[] {0, 0};
}
```

Search each element and check if is the `target - element` in the map, meanwhild, put the element into the map.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `nums`.