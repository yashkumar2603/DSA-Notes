We need the minimum insertions, we can always make n insertions and make it a palindrome by appending the reverse to the back. But we want better than that.
What we do is we take the string, find out the longest palindromic subsequence, then we take the remainders and distribute it on both sides of the string.
ans = n-LPS
```C++
class Solution {
public:
    int dp[501][501];
    int func(string s, string ss, int i, int j) {
        if (i < 0 || j < 0)
            return 0;
        if(dp[i][j]!=-1) return dp[i][j];
        if (s[i] == ss[j])
            return dp[i][j] = 1 + func(s, ss, i - 1, j - 1);
        else
            return dp[i][j] = max(func(s, ss, i - 1, j), func(s, ss, i, j - 1));
    }
    int minInsertions(string s) {
        int n = s.size();
        memset(dp, -1, sizeof(dp));
        string ss = s;
        reverse(s.begin(), s.end());
        return n-func(s, ss, n - 1, n - 1);
    }
};
```

