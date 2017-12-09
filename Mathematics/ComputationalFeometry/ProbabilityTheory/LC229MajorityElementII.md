# LC229. Majority Element II

### LeetCode

## Question

Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times. The algorithm should run in linear time and in O(1) space.

## Solutions

* C++1
```
vector<int> majorityElement(vector<int>& nums) {
    int ele1=1, ele2=2, count1=0, count2=0;
    for(int num : nums)
    {
        if(num == ele1) count1++;
        else if(num == ele2) count2++;
        else if(count1 == 0)
        {
            ele1 = num;
            count1++;
        }
        else if(count2 == 0)
        {
            ele2 = num;
            count2++;
        }
        else
        {
            count1--;
            count2--;
        }
    }
    count1=count2=0;
    for(int num : nums)
    {
        if(num == ele1) count1++;
        else if(num==ele2) count2++;
    }
    vector<int> res;
    if(count1 > nums.size()/3) res.push_back(ele1);
    if(count2 > nums.size()/3) res.push_back(ele2);
    return res;
}
```

## Explanation

**Solution 1:**

Sort the array, cout the two most appeared elements to see if they are appear more than ⌊ n/3 ⌋ times. 

But this solution is not running in linear time and in O(1) space.

* **worst-case time complexity:** O(n*log(n))
* **worst-case space complexity:** O(n*log(n))

**Solution 1:**

Using Moore Voting algorithm to find the two most appeared elements, and count the appeared times.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)
