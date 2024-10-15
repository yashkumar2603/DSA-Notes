# Done 
[Coin Change - LeetCode](https://leetcode.com/problems/coin-change/)

we have to convert the `func(amount-coin, coins)+1LL` to long long by adding 1LL and to match  that in min function, we must also change the ans to long long by adding 0LL
```C++
class Solution {
public:
    int dp[10010];
    int func(int amount, vector<int>& coins)
    {
        if(amount==0) return 0;
        if(dp[amount] != -1) return dp[amount];
        int ans = INT_MAX;

        for(int coin : coins){
            if(amount-coin>=0)
            {
                ans = min(ans + 0LL, func(amount-coin, coins)+1LL);
            }
        }
        return dp[amount] = ans;
    }
    int coinChange(vector<int>& coins, int amount) {
        memset(dp, -1, sizeof(dp));
        if(func(amount, coins)>= INT_MAX) return -1;
        return func(amount, coins);
    }
};
```
