# LC207. Course Schedule

### LeetCode

## Question

There are a total of n courses you have to take, labeled from 0 to n - 1.
Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

**For example:**

`2, [[1,0]]`

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

`2, [[1,0],[0,1]]`

There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

**Note:**

1. The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about <a href="https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs">how a graph is represented</a>.
2. You may assume that there are no duplicate edges in the input prerequisites.


**Hints:**

1. This problem is equivalent to finding if a cycle exists in a directed graph. If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.
2. <a href="https://www.coursera.org/specializations/algorithms">Topological Sort via DFS</a> - A great video tutorial (21 minutes) on Coursera explaining the basic concepts of Topological Sort.
3. Topological sort could also be done <a href="https://en.wikipedia.org/wiki/Topological_sorting#Algorithms">via BFS</a>.

## Solutions

* C++1
```
bool canFinish(int numCourses, vector<pair<int, int>>& prerequisites) {
        vector<vector<int>> map(numCourses, vector<int>());
        vector<int> count(numCourses);
        queue<int> bfsQ;
        for(auto prere : prerequisites)
        {
            map[prere.second].push_back(prere.first); //map prerequisites course to next courses
            count[prere.first]++; //required num of prerequist courses
        }
        for(int i=0; i<numCourses; ++i)
            if(count[i]==0) bfsQ.push(i); //push in the courses wiout prerequisites
            
        int num = 0;
        while(!bfsQ.empty())
        {
            int course = bfsQ.front();
            bfsQ.pop();
            num++;
            for(int nextCourse : map[course])
                if(--count[nextCourse] == 0) bfsQ.push(nextCourse); //reduce 1 prerequisite courses from nextCourse
        }
        return num==numCourses;
}
```

* C++2
```
bool canFinish(int numCourses, vector<pair<int, int>>& prerequisites) {
        vector<vector<int>> graph(numCourses);
        vector<int> preNum(numCourses, 0);
        stack<int> sq; //DFS
        //queue<int> sq; //
        int count=0;

        //preprocessing
        for(auto req : prerequisites)
        {
            graph[req.second].push_back(req.first); //collect all limited courses by req.second
            preNum[req.first]++; // number of courses needed to be finished before req.first
        }
        //put avaliable courses in the stack
        for(int i=0; i<numCourses; ++i)
        {
            if(preNum[i]==0) sq.push(i); //avaliable to take
        }
        //start to take course one by one
        while(!sq.empty())
        {
            int course = sq.top();
            sq.pop();                    //take one course
            count++;                    
            for(auto c : graph[course]) //released courses after taking the course
            {
                if(--preNum[c]==0) sq.push(c); //no prerequist, avaliable to take
            }
        }
        return count==numCourses;
    }
```

## Explanation

1. Map prerequisited courses of a course to the course
2. Count the number of the prerequisited courses of the course
3. Starting from the courses which doesn't need prerequisited courses
4. Take one course `A`. Remove the course `A` from those courses whose prerequisited courses include the course `A`.
5. If a course's prerequisited courses are all took, take the course
6. Finally, check if all courses are took.