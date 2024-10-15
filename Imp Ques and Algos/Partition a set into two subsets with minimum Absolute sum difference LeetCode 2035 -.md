<font color="#f79646">ASKED IN ALL MAJOR COMPANIES</font>
[Partition Array Into Two Arrays to Minimize Sum Difference - LeetCode](https://leetcode.com/problems/partition-array-into-two-arrays-to-minimize-sum-difference/description/)
Same as apple division problem, CSES problem-set, also a meet in the middle problem in CSES.
[[CSES Problem set Notes -]]

### LeetCode Question approach using Meet In the Middle algorithm -
[[Meet In the middle]]

## Correct approach for this problem, but LeetCode is shit, so it wants 2 arrays of size n/2 not arbitrary size arrays.

So basically the method to solve this problem is that once we know what the total sum of the array is,  we just need to make a subset out of it, this will allow us to get the sum of the other subset automatically as that will just be $total sum-subset sum$. Now, we need to see for each value from 0 to total sum that if we can make a subset with that sum or not . To do this we use our concept of subset with sum k code. This returns us  true and false values of whether it is possible or not. 
It returns the value in a grid as `dp[index][target]` so we know that if we take the elements till this index and my target in this, then is it possible to have such a subset or not. Using this we can filter the cases from (0, total sum) to a few of those possibilities, now we just have to subtract the current subset sum from total sum to get the sum of the other subset, then check for the minimum difference they will have.
In this, the subsets will start mirroring after index crosses n/2, so we can just take the final answer check up to n/2 and that will give us our answer.
![[Pasted image 20240506091357.png|750]]
This explains the grid of possibilities returned by the subset with sum k function. 

<font color="#f79646">Code -</font>
```C++
// Function to solve the subset sum problem with memoization
bool subsetSumUtil(int ind, int target, vector<int>& arr, vector<vector<int>>& dp) {
    // Base case: If the target sum is 0, return true
    if (target == 0)
        return dp[ind][target] = true;

    // Base case: If we have considered all elements and the target is still not 0, return false
    if (ind == 0)
        return dp[ind][target] = (arr[0] == target);

    // If the result for this state is already calculated, return it
    if (dp[ind][target] != -1)
        return dp[ind][target];

    // Recursive cases
    // 1. Exclude the current element
    bool notTaken = subsetSumUtil(ind - 1, target, arr, dp);

    // 2. Include the current element if it doesn't exceed the target
    bool taken = false;
    if (arr[ind] <= target)
        taken = subsetSumUtil(ind - 1, target - arr[ind], arr, dp);

    // Store the result in the DP table and return
    return dp[ind][target] = notTaken || taken;
}
```

This is for the subset with sum k function then we have to take these values and place it our grid. The dp array we pass in will get filled with those values and will be available to us after calling the function.

```C++
// Function to find the minimum absolute difference between two subset sums
int minSubsetSumDifference(vector<int>& arr, int n) {
    int totSum = 0;

    // Calculate the total sum of the array
    for (int i = 0; i < n; i++) {
        totSum += arr[i];
    }

    // Initialize a DP table to store the results of the subset sum problem
    vector<vector<int>> dp(n, vector<int>(totSum + 1, -1));

    // Calculate the subset sum for each possible sum from 0 to the total sum
    for (int i = 0; i <= totSum; i++) {
        bool dummy = subsetSumUtil(n - 1, i, arr, dp);   //just call the function to get the dp array filled with the possibilities. for each target value.
    }

    int mini = 1e9;
    for (int i = 0; i <= totSum; i++) {
        if (dp[n - 1][i] == true) {
            int diff = abs(i - (totSum - i));
            mini = min(mini, diff);
        }
    }
    return mini;
}
```

Time Complexity - 
$O(N \times Total Sum) + O(N) + O(N)$ 
The first term comes from the loop where we call for each target sum the Util function.



