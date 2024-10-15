# Done
https://www.youtube.com/watch?v=g8WeLWNRL1A
Solution 
[Minimum Number of Arrows to Burst Balloons - LeetCode](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/?envType=daily-question&envId=2024-03-18)
Question
```C++
bool comp(vector<int>& x, vector<int>& y) { return x[1] < y[1]; }
class Solution {
public:
    int findMinArrowShots(vector<vector<int>>& points) {
        int n = points.size();
        if (n == 0)
            return 0;
        if (n == 1)
            return 1;
            
        int ans = 1;
        int prev;
        sort(points.begin(), points.end(), comp);
        prev = points[0][1];
        for (int i = 0; i < n; i++) {
            if (points[i][0] <= prev) // overlapping(1 arrow needed)
            {
                continue;
            }
            ans++;
            prev = points[i][1];
        }
        return ans;
    }
};
```
We basically sort the balloons based on their ending points. Then we take a previous ending variable. if the start of the next one lies inside or on the boundary of the previous ending, we do nothing as we can pop it with one arrow.
Otherwise we add an arrow and change the previous to the new last element.

