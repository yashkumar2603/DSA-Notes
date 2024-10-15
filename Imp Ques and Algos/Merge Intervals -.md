# Done
This problem asks us to merge all the overlapping intervals that are there in the intervals array, we take the first interval start and end in separate variables. then we compare the beginning of the 2nd interval with the prevEnd, if the next start is smaller then the intervals overlap. 
Otherwise we push the previous interval to the answer using the prevEnd and prevStart values. and allocate them to the next interval to continue checking. 
In the end, we must push the prevStart and prevEnd variables separately so that in the case that the final interval is not overlapping, still it is added to the answer. 

```C++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> ans;
        int prevStart = intervals[0][0];
        int prevEnd = intervals[0][1];
        for(int i=1; i<intervals.size(); i++)
        {
            if(intervals[i][0]<=prevEnd)
            {
                prevEnd = max(prevEnd, intervals[i][1]);
                prevStart = min(prevStart, intervals[i][0]);
            }
            else
            {
                ans.push_back({prevStart, prevEnd});
                prevStart = intervals[i][0];
                prevEnd = intervals[i][1];
            }
        }
        ans.push_back({prevStart, prevEnd});
        return ans;
    }
};
```

