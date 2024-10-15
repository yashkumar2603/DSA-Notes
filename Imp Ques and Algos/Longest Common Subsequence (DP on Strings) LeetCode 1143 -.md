# Done
subsequence are those subsets of the string where the elements may or may not be consecutive, but their order is the same as in the original string.
We take the function and build it so we have 2 parameter, i and j. i records the position of our comparison pointer in the first string and j in the second string. If $s1[i] = s2[j]$ we have found a subsequence of length 1 common, so we call $1+func(i-1, j-1)$ 
If we dont find characters at the i and j values equal, we call  $0+max(func(i-1, j), func(i, j-1))$  which then proceeds to give the solution,  the base case being that if i or j anyone reaches <0, then exit. 
Now , the dp states are i and j only, write the memoization.
```C++
class Solution {
public:
    // Function to find the length of the Longest Common Subsequence (LCS)
    int lcsUtil(string& s1, string& s2, int ind1, int ind2, vector<vector<int>>& dp) {
        // Base case: If either string reaches the end, return 0
        if (ind1 < 0 || ind2 < 0)
            return 0;

        // If the result for this pair of indices is already calculated, return it
        if (dp[ind1][ind2] != -1)
            return dp[ind1][ind2];

        // If the characters at the current indices match, increment the LCS length
        if (s1[ind1] == s2[ind2])
            return dp[ind1][ind2] = 1 + lcsUtil(s1, s2, ind1 - 1, ind2 - 1, dp);
        else
            // If the characters don't match, consider two options: moving either left or up in the strings
            return dp[ind1][ind2] = max(lcsUtil(s1, s2, ind1, ind2 - 1, dp), lcsUtil(s1, s2, ind1 - 1, ind2, dp));
    }

    // Function to calculate the length of the Longest Common Subsequence
    int longestCommonSubsequence(string s1, string s2) {
        int n = s1.size();
        int m = s2.size();
    
        vector<vector<int>> dp(n, vector<int>(m, -1)); // Create a DP table
        return lcsUtil(s1, s2, n - 1, m - 1, dp);
    }
};
```
