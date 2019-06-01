# LC134. Gas Station

### LeetCode

## Question

There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

Note:

The solution is guaranteed to be unique.

## Solutions

### Solution 1

* C++
```
int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
    int start=0, tank=0, mostLackGas = INT_MAX, n = gas.size();
    for(int i=0; i<n; ++i)
    {
        tank += gas[i]-cost[i];
        if(tank<mostLackGas) 
        {
            mostLackGas = tank;
            start = i+1; //pass the most lack gas road
        }
    }
    return tank<0 ? -1 : (start%n);
}
```

As long as the total of gas is larger than the total cost, you can travel around the circuit once at least. Because the solution is guaranteed to be unique, so the total of gas should be close to the total cost.

The solution is to leave the station of most lack gas to the end of the circular journey. So the next station of the most lack gas station will could be the starting gas station.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `gas`.
* **worst-case space complexity:** `O(1)`.
