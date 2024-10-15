[Coin Change II - LeetCode](https://leetcode.com/problems/coin-change-ii/)

somewhat similar to questions where all possible cases which satisfy some condition is asked.

```C++
class Solution {
public:
    int dp[310][5010];
    int func(int ind, int amount, vector<int>& coins) {
        if (amount == 0)
            return 1;
        if (ind < 0)
            return 0; // basically exhausted all coins, but still not reached
                      // the desired amount
        if (dp[ind][amount] != -1)
            return dp[ind][amount];
        int ans = 0;
        for (int coin_amount=0; coin_amount <= amount; coin_amount += coins[ind]) {
            ans += func(ind - 1, amount - coin_amount, coins);
        }
        return dp[ind][amount] = ans;
    }
    int change(int amount, vector<int>& coins) {
        memset(dp, -1, sizeof(dp));
        return func(coins.size() - 1, amount, coins);
    }
};
```