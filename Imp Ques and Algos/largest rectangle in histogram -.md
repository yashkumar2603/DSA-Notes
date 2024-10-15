https://www.youtube.com/watch?v=zx5Sw9130L0 - best explanation, cant be better.
# DONE
```C++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int n=heights.size();
        int start;
        int ans=0;
        stack<pair<int, int>> s;
        for(int i=0; i<n; i++)
        {
            start=i;
            while(!s.empty() && s.top().second>heights[i])
            {
                pair<int, int> curr;
                curr = s.top();
                s.pop();

                ans=max(ans, curr.second*(i-curr.first));
                start = curr.first;
            }
            s.push(make_pair(start, heights[i]));
        }
        while(!s.empty())
        {
            ans=max(ans, s.top().second*(n-s.top().first));
            s.pop();
        }

        return ans;
    }
};

```