# LC599. Minimum Index Sum of Two Lists

### LeetCode

## Question

Suppose Andy and Doris want to choose a restaurant for dinner, and they both have a list of favorite restaurants represented by strings.

You need to help them find out their common interest with the least list index sum. If there is a choice tie between answers, output all of them with no order requirement. You could assume there always exists an answer.

**Example 1:**

```
Input:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
Output: ["Shogun"]
Explanation: The only restaurant they both like is "Shogun".
```

**Example 2:**

```
Input:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["KFC", "Shogun", "Burger King"]
Output: ["Shogun"]
Explanation: The restaurant they both like and have the least index sum is "Shogun" with index sum 1 (0+1).
```

**Note:**

1.  The length of both lists will be in the range of [1, 1000].
2.  The length of strings in both lists will be in the range of [1, 30].
3.  The index is starting from 0 to the list length minus 1.
4.  No duplicates in both lists.

## Solutions

### Solution 1

* C++
```
vector<string> findRestaurant(vector<string>& list1, vector<string>& list2) {
    unordered_map<string, int> map1, map2, commonMap;
    for(int i=0; i<list1.size(); ++i)
        map1[list1[i]] = i;
    for(int j=0; j<list2.size(); ++j)
        map2[list2[j]] = j;
    
    int indexSum = 2000;
    for(string r : list1) //we can use for(int i=0; i<list1.size(); i++)
    {
        if(map2.count(r) > 0)
        {
            commonMap[r] = map1[r] + map2[r]; //no need to use map1
            indexSum = min(indexSum, commonMap[r]);
        }
    }
    
    vector<string> res;
    for(auto id : commonMap)
        if(id.second == indexSum)
            res.push_back(id.first);
    return res;
}
```

1. Using a map to map the first list's restaurant names to their locations.
2. Check the second restaurant list, based on the map of the first restaurant list, find the minimum index sum of common interest.
3. Based on the minimum index sum, check the second restaurant list again, find all restaurant with the minimum index sum.

**Complexity:**

* **worst-case time complexity:** `O(max(n1, n2))` where `n1` is the length of the `list1`, `n2` is the length of the `list2`.
* **worst-case space complexity:** O(max(n1, n2))` where `n1` is the length of the `list1`, `n2` is the length of the `list2`.
