## Distinct Subsequences - 
https://leetcode.com/problems/distinct-subsequences/description/
We take a function f(i, j) and that means, the number of subsequences in s1(0....i) equal to s2(0....j).
Now, if the elements match, we take sum of f(i-1, j-1)(select the matching element)+f(i-1, j)(dont select the matching element)
and if they dont match f(i-1, j)
in the base case, if j<0 -> full string used and matched -> return 1;
if i<0 -> full string exhausted, but matching didn't happen fully-> return 0;

```C++
class Solution {
public:
    const int prime = 1e9 + 7;
    // Function to count the number of distinct subsequences of s2 in s1
    int countUtil(string s1, string s2, int ind1, int ind2,
                  vector<vector<int>>& dp) {
        // If s2 has been completely matched, return 1 (found a valid
        // subsequence)
        if (ind2 < 0)
            return 1;
        // If s1 has been completely traversed but s2 hasn't, return 0
        if (ind1 < 0)
            return 0;
        // If the result for this state has already been calculated, return it
        if (dp[ind1][ind2] != -1)
            return dp[ind1][ind2];
        int result = 0;
        // If the characters match, consider two options: either leave one
        // character in s1 and s2 or leave one character in s1 and continue
        // matching s2
        if (s1[ind1] == s2[ind2]) {
            int leaveOne = countUtil(s1, s2, ind1 - 1, ind2 - 1, dp);
            int stay = countUtil(s1, s2, ind1 - 1, ind2, dp);
            result = (leaveOne + stay);
        } else {
            // If characters don't match, just leave one character in s1 and
            // continue matching s2
            result = countUtil(s1, s2, ind1 - 1, ind2, dp);
        }
        // Store the result and return it
        dp[ind1][ind2] = result;
        return result;
    }
    int numDistinct(string s, string t) {
        int n = s.size(), m = t.size();
        vector<vector<int>> dp(n + 1, vector<int>(m + 1, -1));
        return countUtil(s, t, n, m, dp);
    }
};
```