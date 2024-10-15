# Done
## longest increasing subsequence (vanilla)
dp states - index and prev_index(index of the previous number, so that we can check for increasing)
```C++
int f(int ind, int p_ind, int n, vector<int>& arr, vector<vector<int>>& dp) 
    {
        if (ind == n)
            return 0;
        if(dp[ind+1][p_ind+1]!=-1) return dp[ind+1][p_ind+1];
        int len = 0 + f(ind + 1, p_ind,n,arr, dp); // dont-take case
        if (p_ind == -1 || arr[ind] > arr[p_ind])
            len = max(len, 1 + f(ind + 1, ind,n,arr, dp)); // take
        return dp[ind+1][p_ind+1] = len;
    }
 int lengthOfLIS(vector<int>& nums){ 
    int n=nums.size();
    vector<vector<int>> dp(n+2, vector<int>(n+2,-1));
    return f(0,-1, n, nums, dp);
}
```

## largest divisible Subset - 
```C++
class Solution {
public:
    vector<int> f(int ind, int p_ind, vector<int>& nums, vector<vector<vector<int>>>& dp) {
        int n = nums.size();
        if (ind == n) return {}; // Base case: reached end of nums
        if (dp[ind][p_ind + 1].size() != 0) return dp[ind][p_ind + 1];
        
        vector<int> not_take = f(ind + 1, p_ind, nums, dp); // Skip current number
        vector<int> take;

        if (p_ind == -1 || nums[ind] % nums[p_ind] == 0) {
            take = f(ind + 1, ind, nums, dp);
            take.push_back(nums[ind]); // Include current number
        }
        // Choose the larger subset between 'take' and 'not_take'
        vector<int> ans = (take.size() > not_take.size()) ? take : not_take;
        return dp[ind][p_ind + 1] = ans; // Memoize and return result
    }
    
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        int n = nums.size();
        if (n == 0) return {};
        sort(nums.begin(), nums.end()); // Sort to ensure divisibility condition
        // DP array for memoization. Using vector of vectors of vectors for storing intermediate results.
        vector<vector<vector<int>>> dp(n, vector<vector<int>>(n + 1));
        vector<int> res = f(0, -1, nums, dp);
        return res;
    }
};
THIS IS CORRECT BUT WONT PASS THE SUBMISSION AS JUST A VERY TINY BIT SLOWER.
```

