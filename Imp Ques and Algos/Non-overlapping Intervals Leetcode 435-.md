First we detect the overlap in any intervals by checking if an interval starts before one ends and if so, we are going to delete the one with the larger ending time value. This helps us in accomplishing the target of deleting the fewest possible number of intervals.
To accomplish all this, the timeline array must be sorted in ascending order based on the start time of the intervals.
So the total time complexity = $O(nlogn) + O(n) \approx O(nlogn)$
# Done
```C++
class Solution {
public:
//greedy solution
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());
        int count=0;
        int prevEnd = intervals[0][1];
        for(int i=1; i<intervals.size(); i++)
        {
            if(intervals[i][0]<prevEnd)
            {
                count++;
                prevEnd = min(prevEnd, intervals[i][1]);
            }
            else
            {
                prevEnd = intervals[i][1];
            }
        }
        return count;
    }
};
```
