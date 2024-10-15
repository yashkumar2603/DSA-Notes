https://leetcode.com/problems/student-attendance-record-ii/description/?envType=daily-question&envId=2024-05-26
# Done
```C++
#define MOD 1000000007
class Solution {
public:
    int dp[100001][3][3];
    // ac is the *total* absent count, clc is the consecutive late count.
    int solve(int n, int ac, int clc) {
        if (n == 0)
            return 1;
        long long ans=0;

        if (dp[n][ac][clc] != -1)
            return dp[n][ac][clc];
        ans = (solve(n - 1, ac, 0))% MOD;
        if (ac < 1)
            ans = (ans+solve(n - 1, ac + 1, 0)) % MOD;
        if (clc < 2)
            ans = (ans+solve(n - 1, ac, clc + 1)) % MOD;
        return dp[n][ac][clc] = ans%MOD;
    }
    int checkRecord(int n) {
        memset(dp, -1, sizeof(dp));
        return solve(n, 0, 0);
    }
};
```