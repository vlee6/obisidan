A greedy algorithm picks things at greatest convenience.

For example, see the interval scheduling optimization problem: given a set of time intervals, `int-sch-opt` asks us to find set of non-overlapping time intervals of maximal size

*`int-sch-opt` computational problem* 
**Input:** $[a_0,b_o],...,[a_{n-1} ,b_{n-1}]$
**Output:** A set of time non-overlapping time intervals

### Greedy algorithm for `int-sch-opt` 
A greedy algorithm sorts the intervals in increasing order by end times using merge sort. Then create set of intervals $S$. Starting from the interval with the earliest end time to the interval with the latest end time, if none of the intervals in $S$ conflict with the selected interval, add it to $S$.

This finds the largest non conflicting set of intervals in $O(n \log n)$ time because of merge sort.