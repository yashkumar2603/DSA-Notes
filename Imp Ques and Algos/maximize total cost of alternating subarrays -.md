[Maximize Total Cost of Alternating Subarrays - LeetCode](https://leetcode.com/contest/weekly-contest-403/problems/maximize-total-cost-of-alternating-subarrays/)
Take/not take dp
isStart marks if it is a new subarray or continued.
sign is for +/- conversion.
# Done
```C++

class Solution {
public:
    long long solve(int i, int isStart, int sign, vector<int>& nums, vector<vector<vector<long long>>>& dp)
    {
        if(i==nums.size()) return 0;

        if(dp[i][isStart][sign]!=-1e15) return dp[i][isStart][sign];

        long long ans = -1e15;
        if(isStart ==0)
        {
            ans=max(ans, nums[i]+solve(i+1, 1, sign^1, nums, dp));//have to take as new subarray.
        }else{
            if(sign==1){
                ans=max(ans, -nums[i]+solve(i+1, 1, sign^1, nums, dp));//take
                ans=max(ans, solve(i,0,0,nums,dp));//not take
            }
            else{
                ans = max(ans, nums[i]+solve(i+1, 1, sign^1, nums,dp));//take
                ans=max(ans, solve(i,0,0,nums,dp));//not take
            }
        }
        return dp[i][isStart][sign] = ans;
    }
    long long maximumTotalCost(vector<int>& nums) {
        int n= nums.size();
        vector<vector<vector<long long>>> dp(n+1, vector<vector<long long>>(2, vector<long long>(2, -1e15)));

        return solve(0,0,0,nums, dp);
    }
};
```

