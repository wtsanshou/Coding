# LC169. Majority Element

### LeetCode

## Question

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

## Solutions

* C++1 (22ms)
```
int majorityElement(vector<int>& nums) {
    int count=0, res;
    for(int i=0; i<nums.size(); ++i)
    {
        if(count==0) res = nums[i];
        if(nums[i] == res) count++;
        else count--;
    }
    return res;
}
```

* C++2 (44ms)
```
int majorityElement(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    return nums[nums.size()/2];
}
```

* C++3 (179ms)
```
int majorityElement(vector<int>& nums) {
    nth_element(nums.begin(), nums.begin()+nums.size()/2, nums.end());
    return nums[nums.size()/2];
}
```

* Java1 (3ms)
```
public int majorityElement(int[] nums) {
    Arrays.sort(nums);
    return nums[nums.length/2];
}
```

* Java2 (44ms)
```
public int majorityElement(int[] nums) {
    int half = nums.length/2;
    Map<Integer, Integer> count = new HashMap();
    for(int n : nums)
    {
        if(!count.containsKey(n))  count.put(n, 1);
        else  count.put(n, count.get(n) + 1);
        if(count.get(n)>half) return n;
    }
    return 0;
}
```

## Explanation

Solution 1: Moore Voting algorithm. 

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)

Solution 2: sort the array, the element in the middle of the array is the majority element.

* **worst-case time complexity:** O(n*log(n))
* **worst-case space complexity:** O(n*log(n))

Solution 3: Using a hash map to count the number of each element.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)
