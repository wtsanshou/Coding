# LC399. Evaluate Division

### LeetCode

## Question

Equations are given in the format A / B = k, where A and B are variables represented as strings, and k is a real number (floating point number). Given some queries, return the answers. If the answer does not exist, return -1.0.

**Example:**

Given a / b = 2.0, b / c = 3.0. 

queries are: a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ? . 

return [6.0, 0.5, -1.0, 1.0, -1.0 ].

The input is: `vector<pair<string, string>> equations`, `vector<double>& values`, `vector<pair<string, string>> queries`, where `equations.size() == values.size()`, and the values are positive. This represents the equations. Return `vector<double>`.

According to the example above:
```
equations = [ ["a", "b"], ["b", "c"] ],
values = [2.0, 3.0],
queries = [ ["a", "c"], ["b", "a"], ["a", "e"], ["a", "a"], ["x", "x"] ]. 
```

The input is always valid. You may assume that evaluating the queries will result in no division by zero and there is no contradiction.

## Solutions
* C++1 (3ms)
```bash
class Solution {
public:
    double search(string left, string right, unordered_map<string, unordered_map<string, double>>& graph, unordered_set<string>& set)
    {
        if(graph[left].find(right)!=graph[left].end()) return graph[left][right]; //find it in graph
        for(auto g : graph[left])
        {
            if(set.find(g.first) == set.end()) //not visited yet
            {
                set.insert(g.first); //mark visit
                double temp = search(g.first, right, graph, set);
                if(temp>0) return temp*g.second;
            }
        }
        return 0;
    }

    vector<double> calcEquation(vector<pair<string, string>> equations, vector<double>& values, vector<pair<string, string>> queries) {
        unordered_map<string, unordered_map<string, double>> graph;
        vector<double> ans;
        for(int i=0; i<values.size(); ++i)
        {
            graph[equations[i].first].insert(make_pair(equations[i].second, values[i])); //create graphs
            graph[equations[i].second].insert(make_pair(equations[i].first, 1.0/values[i])); // values are all positive
        }
        
        for(auto q : queries)
        {
            unordered_set<string> set;
            double temp = search(q.first, q.second, graph, set);
            ans.push_back( (temp>0) ? temp : -1.0);
        }
        return ans;
    }
};
```

