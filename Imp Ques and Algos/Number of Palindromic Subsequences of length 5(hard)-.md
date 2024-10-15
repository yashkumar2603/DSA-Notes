[Count Palindromic Subsequences - LeetCode](https://leetcode.com/problems/count-palindromic-subsequences/description/)
- - `fr` and `sec`: the first and second characters of the current subsequence (0 or 1).
    - `len`: the current length of the subsequence.
    - `i`: the current index in the string `s`.
`solve` function
This function recursively calculates the number of palindromic subsequences starting from index `i` in the string `s` with the given `fr`, `sec`, and `len`.
- **Base cases:**
    - If the length of the subsequence reaches 5, it's a palindrome, so return 1.
    - If we reach the end of the string, there are no more subsequences, so return 0.
    - If the result is already calculated for the given parameters, return it from the `dp` table.
- **Recursive cases:**
    - `op1`: The number of palindromic subsequences if the current character `s[i]` becomes the first character of the next subsequence.
    - `op2`: The number of palindromic subsequences if the current character `s[i]` becomes the second character of the next subsequence.
    - `op3`: The number of palindromic subsequences if the current character is not added to the subsequence.
    - `op4`: The number of palindromic subsequences if the current character is added to the subsequence and it matches the second character.
    - `op5`: The number of palindromic subsequences if the current character is added to the subsequence and it matches the first character.
    - `op6`: The number of palindromic subsequences if the current character is not added to the subsequence and the length remains the same.

```C++
class Solution {
public:
    int mod = 1e9 + 7;
    int solve(int i,string &s,char fr,char sec,int len, vector<vector<vector<vector<int>>>> &dp){
        if(len == 5) return 1;
        if(i == s.size()) return 0;
        if(dp[fr-'0'][sec - '0'][len][i] != -1) return dp[fr-'0'][sec - '0'][len][i];
        
        long long op1 = 0, op2 = 0, op3 = 0, op4 = 0,op5 = 0;
        if(len == 0) op1 = solve(i+1,s,s[i],sec,len+1,dp);
        if(len == 1) op2 = solve(i+1,s,fr,s[i],len+1,dp);
        if(len == 2) op3 = solve(i+1,s,fr,sec,len+1,dp);
        if(len == 3 and s[i] == sec) op4 = solve(i+1,s,fr,sec,len+1,dp);
        if(len == 4 and s[i] == fr) op5 = solve(i+1,s,fr,sec,len+1,dp);
        long long op6 = solve(i+1,s,fr,sec,len,dp);
        
        return dp[fr-'0'][sec - '0'][len][i] = (op1 + op2 + op3 + op4 + op5 + op6) % mod;
    }
    int countPalindromes(string s) {
        vector<vector<vector<vector<int>>>> dp(10, vector<vector<vector<int>>> (10, vector<vector<int>> (5,vector<int>(s.size(),-1))));
        return solve(0,s,'1','1',0,dp);
    }
};
```