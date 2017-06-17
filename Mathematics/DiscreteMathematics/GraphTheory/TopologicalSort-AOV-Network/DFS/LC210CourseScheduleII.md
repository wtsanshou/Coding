# LC210. Course Schedule II

### LeetCode

## Question

There are a total of n courses you have to take, labeled from 0 to n - 1.
Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

**For example:**

`2, [[1,0]]`

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1]

`4, [[1,0],[2,0],[3,1],[3,2]]`

There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is [0,1,2,3]. Another correct ordering is[0,2,1,3].

**Note:**

1.  The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.
2.  You may assume that there are no duplicate edges in the input prerequisites.

**Hints:**

1.  This problem is equivalent to finding the topological order in a directed graph. If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.
2.  Topological Sort via DFS - A great video tutorial (21 minutes) on Coursera explaining the basic concepts of Topological Sort.
3.  Topological sort could also be done via BFS.

## Solutions

* C++1
```
vector<int> findOrder(int numCourses, vector<pair<int, int>>& prerequisites) {
        vector<vector<int>> graph(numCourses);
        vector<int> countPrereq(numCourses), res;
        stack<int> sta;
        for(auto prere : prerequisites)
        {
            graph[prere.second].push_back(prere.first);
            countPrereq[prere.first]++;
        }
        for(int i=0; i<numCourses; ++i)
            if(countPrereq[i]==0) sta.push(i);
        while(!sta.empty())
        {
            int course = sta.top();
            sta.pop();
            res.push_back(course);
            for(int next : graph[course])
                if(--countPrereq[next]==0) sta.push(next);
        }
        return res.size()==numCourses ? res : vector<int>();
}
```

* C++2
```
vector<int> findOrder(int numCourses, vector<pair<int, int>>& prerequisites) {
        vector<vector<int>> graph(numCourses);
        vector<int> preNum(numCourses), res;
        //stack<int> sq; //DFS
        queue<int> sq; //BFS

        //preprocessing
        for(auto req : prerequisites)
        {
            //collect all limited courses by req.second
            graph[req.second].push_back(req.first);
            //number of courses needed to be finished before req.first
            preNum[req.first]++;
        }

        //put avaliable courses in the stack
        for(int i=0; i<numCourses; ++i)
        {
            if(preNum[i]==0) sq.push(i); //avaliable to take
        }

        //start to take course one by one
        while(!sq.empty())
        {
            //take one course
            int course = sq.front();
            sq.pop();                   
            res.push_back(course);
            //released courses after taking the course                 
            for(auto c : graph[course])
            {
                //no prerequist, avaliable to take
                if(--preNum[c]==0) sq.push(c); 
            }
        }
        return res.size()==numCourses ? res : vector<int>();
    }
```

## Explanation

The same idea of <a href="LC207CourseSchedule.md">LC207. Course Schedule</a>. 

Push the crouse to the result array when you take a available course.