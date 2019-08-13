# Dynamic Programming

Dynamic Programming is mainly an optimization over plain recursion. Wherever we see a recursive solution that has repeated calls for same inputs, we can optimize it using Dynamic Programming. The idea is to simply store the results of subproblems, so that we do not have to re-compute them when needed later.

## Template

**State**

* Maximum
* Minimum
* Best Option
* True/False
* Count(something)

**Function**

Parent question is transfered by `n` sub questions in some ways.

**Initialization**

The smallest state or the starting point.

**Result**

The biggest state or the ending point.
