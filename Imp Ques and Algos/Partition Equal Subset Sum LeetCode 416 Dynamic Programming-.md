[Partition Equal Subset Sum - LeetCode](https://leetcode.com/problems/partition-equal-subset-sum/)

```C++
class Solution {
public:
    int dp[205][20005];
    bool func(int i, int sum, vector<int>& nums) {
        if (sum == 0)
            return true; // sum made
        if (i < 0)
            return false; // elements finished but sum not finished.
        if (dp[i][sum] != -1)
            return dp[i][sum];
        // not consider ith index
        int isPossible = func(i - 1, sum, nums);
        // consider the ith index
        if (sum - nums[i] >= 0)
            isPossible |= func(i - 1, sum - nums[i], nums);
        return dp[i][sum] = isPossible;
    }
    bool canPartition(vector<int>& nums) {
        memset(dp, -1, sizeof(dp));
        int sum = accumulate(nums.begin(), nums.end(), 0);
        if (sum % 2 != 0)
            return false;
        sum = sum / 2;
        return func(nums.size() - 1, sum, nums);
    }
};
```