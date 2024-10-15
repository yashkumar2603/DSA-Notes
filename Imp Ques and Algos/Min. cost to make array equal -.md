https://leetcode.com/problems/minimum-cost-to-make-array-equal/
# For later, hard
```C++
class Solution {
public:
    long long minCost(vector<int>& nums, vector<int>& cost) {
        int n = nums.size();
        vector<pair<int, int>> v(n);
        for (int i = 0; i < n; ++i) {
            v[i] = {nums[i], cost[i]};
        }
        sort(v.begin(), v.end());

        vector<long long> prefixCost(n);
        prefixCost[0] = v[0].second;
        for (int i = 1; i < n; ++i) {
            prefixCost[i] = prefixCost[i - 1] + v[i].second;
        }

        long long totalCost = prefixCost[n - 1];
        int medianIdx = 0;
        for (int i = 0; i < n; ++i) {
            if (prefixCost[i] >= (totalCost + 1) / 2) {
                medianIdx = i;
                break;
            }
        }

        int x = v[medianIdx].first;
        long long ans = 0;
        for (int i = 0; i < n; ++i) {
            ans += abs(nums[i] - x) * 1LL * cost[i];
        }

        return ans;
    }
};

```