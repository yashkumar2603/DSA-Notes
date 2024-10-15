https://leetcode.com/problems/most-profit-assigning-work/description/?envType=daily-question&envId=2024-06-18
# Done
we sort both the arrays of pair of (difficulties, profits) and the worker capability. then we make a current max_profit and put the max_profit encountered so far in it(prefix maximum), because we can take even the lowest diffiulty job if its profit is very good. 
Now we just keep moving in workers and checking with a second pointer j in the array of pairs. while worker of  i <= vector of pairs of j.first, we keep finding the max profit, the max profit job is what we take up for the worker, no matter the difficulty if it is easier than the worker's capability. 
Now we keep on adding this max to the answer for each worker.

```C++
class Solution {
public:
    int maxProfitAssignment(vector<int>& difficulty, vector<int>& profit, vector<int>& worker) {
        int n=difficulty.size(); int m=worker.size();
        vector<pair<int, int>> vp;
        for(int i=0; i<n; i++)
        {
            vp.push_back({difficulty[i], profit[i]});
        }
        sort(worker.begin(), worker.end());
        sort(vp.begin(), vp.end());

        int ans=0, ma=0, j=0;

        for(int i=0; i<m; i++)
        {
            while(j<m && vp[j].first<=worker[i])
            {
                ma=max(ma, vp[j].second);
                j++;
            }
            ans+= ma;
        }
        return ans;
    }
};
```

