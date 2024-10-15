# Done
To solve this ,  we can do one thing.
We know how to solve longest common subsequence, in which we find the longest common subsequence in between 2 strings given, here we have to find the longest possible palindromic subsequence in one string. 
To relate these 2, we reverse the string and then apply longest common subsequence on it, the reversal basically makes it so only the palindromic subsequences are selected and hence we get our answer
pseudo code - 
[[Longest Palindromic Subsequence LeetCode -]]
```
int func(string s, i, j)
{
	string ss = reverse(s)
	if(i<0 || j<0) return 0; //length of longest commom subsequence in 0 elements.
	if(s[i]==ss[j]) return 1+func(s, i-1, j-1);
	else return max(func(s, i-1, j), func(s, i, j-1));
}
```
now apply memoization to this and done. 

### Memoization Solution - 
```C++
class Solution {
public:
    int dp[900][900];
    int func(string s, string ss, int i, int j) {
        if (i < 0 || j < 0)
            return 0;
        if(dp[i][j]!=-1) return dp[i][j];
        if (s[i] == ss[j])
            return dp[i][j] = 1 + func(s, ss, i - 1, j - 1);
        else
            return dp[i][j] = max(func(s, ss, i - 1, j), func(s, ss, i, j - 1));
    }
    int longestPalindromeSubseq(string s) {
        int n = s.size();
        memset(dp, -1, sizeof(dp));
        string ss = s;
        reverse(s.begin(), s.end());
        return func(s, ss, n - 1, n - 1);
    }
};
```

This doesn't work, the thing is that we get  a memory limit exceeded error.
We have to apply space optimization to the code to not get it the space limit exceed.
So tabulation needs to be applied.

### Tabulation approach - 

<font color="#f79646">See the Space optimizations video of striver and the tabulation dp video.</font>
```cpp
// Function to calculate the length of the Longest Common Subsequence
int lcs(string s1, string s2) {
    int n = s1.size();
    int m = s2.size();

    // Create a 2D DP array to store the length of the LCS
    vector<vector<int>> dp(n + 1, vector<int>(m + 1, -1));

    // Initialize the first row and first column to 0
    for (int i = 0; i <= n; i++) {
        dp[i][0] = 0;
    }
    for (int i = 0; i <= m; i++) {
        dp[0][i] = 0;
    }

    // Fill in the DP array
    for (int ind1 = 1; ind1 <= n; ind1++) {
        for (int ind2 = 1; ind2 <= m; ind2++) {
            if (s1[ind1 - 1] == s2[ind2 - 1])
                dp[ind1][ind2] = 1 + dp[ind1 - 1][ind2 - 1];
            else
                dp[ind1][ind2] = max(dp[ind1 - 1][ind2], dp[ind1][ind2 - 1]);
        }
    }

    // The value at dp[n][m] contains the length of the LCS
    return dp[n][m];
}

// Function to calculate the length of the Longest Palindromic Subsequence
int longestPalindromeSubsequence(string s) {
    // Create a reversed copy of the string
    string t = s;
    reverse(s.begin(), s.end());

    // Call the LCS function to find the length of the Longest Common Subsequence
    return lcs(s, t);
}
```


