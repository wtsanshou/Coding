# LC599. Minimum Index Sum of Two Lists

### LeetCode

## Question

Suppose Andy and Doris want to choose a restaurant for dinner, and they both have a list of favorite restaurants represented by strings.

You need to help them find out their common interest with the least list index sum. If there is a choice tie between answers, output all of them with no order requirement. You could assume there always exists an answer.

**Example 1:**

**Input:**
```
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
```
**Output:**
`["Shogun"]`

**Explanation:**
`The only restaurant they both like is "Shogun".`

**Example 2:**
**Input:**
```
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["KFC", "Shogun", "Burger King"]
```

**Output:** 
`["Shogun"]`

**Explanation:**

The restaurant they both like and have the least index sum is "Shogun" with index sum 1 (0+1).

**Note:**

1.  The length of both lists will be in the range of [1, 1000].
2.  The length of strings in both lists will be in the range of [1, 30].
3.  The index is starting from 0 to the list length minus 1.
4.  No duplicates in both lists.

## Solutions
* C++1
```
vector<string> findRestaurant(vector<string>& list1, vector<string>& list2) {
        unordered_map<string, int> map1, map2, commonMap;
        for(int i=0; i<list1.size(); ++i)
            map1[list1[i]] = i;
        for(int j=0; j<list2.size(); ++j)
            map2[list2[j]] = j;
        
        int indexSum = 2000;
        for(string r : list1)
        {
            if(map2.count(r) > 0)
            {
                commonMap[r] = map1[r] + map2[r];
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

## Explanation
First, recording the index sum of every common interest into a map `commonMap` and find the minimum index sum `indexSum`.

Then, according to the found minmum index sum `indexSum`, check each restaurant in the map `commonMap`.
