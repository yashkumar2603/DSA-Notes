# Done
**Very Important question, asked in startups all the time, also very hard with respect to strange edge cases it has and stuff. It is annoying in short.**
<span style="background:#d3f8b6">Remember the solution honestly if cant get the understanding.</span>

Basically first we take the easy cases where the new is inserted before or after the current interval without any issue, then its all easy.
if new comes before, we insert the new interval and then the rest after it.(if statement)
if after, we insert the original one until we reach the position of the new one.(else if statement)
Then we take the case in which it overlaps, then take the minimum of the starts and the max of the ends to get the new interval, we keep checking for overlap and merging until the above conditions are fulfilled, then we push into in the answer, not before that.

```C++
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        vector<vector<int>> ans;
        int n= intervals.size();
        for(int i=0; i<n; i++)
        {
            if(newInterval[1]<intervals[i][0])
            {
                ans.push_back(newInterval);
                for(int j = i; j<n; j++)
                    ans.push_back(intervals[j]);
                return ans;
            }
            else if(newInterval[0]>intervals[i][1])
            {
                ans.push_back(intervals[i]);
            }
            else 
            {
                newInterval = {min(newInterval[0], intervals[i][0]), max(newInterval[1], intervals[i][1])};
            }
        }
        ans.push_back(newInterval);
        return ans;
    }
};
```
