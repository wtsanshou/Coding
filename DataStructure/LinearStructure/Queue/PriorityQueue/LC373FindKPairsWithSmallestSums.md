# LC373. Find K Pairs with Smallest Sums

### LeetCode

## Question

You are given two integer arrays `nums1` and `nums2` sorted in ascending order and an integer `k`.

Define a pair `(u,v)` which consists of one element from the first array and one element from the second array.

Find the `k` pairs `(u1,v1),(u2,v2) ...(uk,vk)` with the smallest sums.

**Example 1:**
```
Given nums1 = [1,7,11], nums2 = [2,4,6],  k = 3

Return: [1,2],[1,4],[1,6]

The first 3 pairs are returned from the sequence:
[1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
```

**Example 2:**
```
Given nums1 = [1,1,2], nums2 = [1,2,3],  k = 2

Return: [1,1],[1,1]

The first 2 pairs are returned from the sequence:
[1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]
```

**Example 3:**
```
Given nums1 = [1,2], nums2 = [3],  k = 3 

Return: [1,3],[2,3]

All possible pairs are returned from the sequence:
[1,3],[2,3]
```

## Solutions

* C++1
```
class Solution {
public:
    struct myOper
    {
        bool operator() (pair<int,int>&a, pair<int,int>&b)
        {
            return a.first+a.second < b.first+b.second;
        }
    };
    vector<pair<int, int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {
        vector<pair<int, int>> res;
        int n1=nums1.size(), n2=nums2.size();
        if(n1==0 || n2==0 || k==0) return res;
        priority_queue<pair<int,int>, vector<pair<int,int>>, myOper> pq; 
        for(int i=0; i<min(n1,k); ++i)
        {
            for(int j=0; j<min(n2,k); ++j)
            {
                if(pq.size()<k)
                {
                    pq.push(make_pair(nums1[i], nums2[j]));
                }
                else if(nums1[i]+nums2[j]<pq.top().first + pq.top().second) // Eliminate the maximum pair.
                {
                    pq.pop();
                    pq.push(make_pair(nums1[i], nums2[j]));
                }
            }
        }
        while(!pq.empty())
        {
            res.push_back(pq.top());
            pq.pop();
        }
        return res;
    }
};
```

* C++2
```vector<pair<int, int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {
    int n1=nums1.size(), n2=nums2.size();
    vector<pair<int, int>> res;
    if(n1==0 || n2==0) return res;
    auto mycomp = [&nums1, &nums2](pair<int, int> a, pair<int, int> b) 
        { return nums1[a.first]+nums2[a.second] > nums1[b.first]+nums2[b.second]; };
    priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(mycomp)> min_heap(mycomp);
    min_heap.emplace(0,0);
    //min_heap.push(make_pair(0,0));
    while(res.size()<k && !min_heap.empty())
    {
        pair<int, int> minp = min_heap.top();
        min_heap.pop();
        //res.push_back(make_pair(nums1[minp.first], nums2[minp.second]));
        res.emplace_back(nums1[minp.first], nums2[minp.second]);
        if(minp.first+1<n1)
            min_heap.emplace(minp.first+1, minp.second);
        if(minp.first==0 && minp.second+1<n2)
            min_heap.emplace(0, minp.second+1);
    }
    return res;
}
```

## Explanation

Sum each pair, add them into a size of 'k' min heap.

* **worst-case time complexity:** `O(N1 * N2)`, where `N1` is the length of the `nums1`, `N2` is the length of the `nums2`.
* **worst-case space complexity:** `O(K)`, where `K` is the length the `k` pairs.
