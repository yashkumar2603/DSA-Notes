# Done
Solved Using Recursion only, constraints small so this also gets accepted.
we can add 1 of 2 signs in front of each element, so the total number of possible combinations are hence 2^n.
to bring this to O(n) from O(2^n) we will have to use dp. 
at each number we have two choices, to add a + sign before it or a - sign before it and then going further in the recurrence.
then check if the target finally reaches 0.
choice DP
```C++
class Solution {
public:
    int func(vector<int>& nums, int target, int idx, int current, int count)
    {
        if(idx<0) {
            if(current == target) {count++; return count;}
            return 0;
        }

        int minus = func(nums, target, idx-1, current-nums[idx], count); //subtracted it.
        int plus = func(nums, target, idx-1, current+nums[idx], count);  //added it.

        return minus + plus;  //number of ways from minus and number of ways from plus.
    }

    int findTargetSumWays(vector<int>& nums, int target) {
        return func(nums, target, nums.size()-1, 0, 0);
    }
};
```

The problem with using this approach and then adding memoization to it is that because we have to use all elements of array until end and there's no condition where we can stop the call in the middle. This is more of a backtracking rather than dp.
### Striver's approach (DP is possible in this) - 
The approach relies on the transformation of this problem into the Subarray problems type. 
![[Pasted image 20240504154558.png]]

**Steps to form the recursive solution:** 

**Step 1:** Express the problem in terms of indexes.

The array will have an index but there is one more parameter “target”. We are given the initial problem to find whether there exists in the whole array a subsequence whose sum is equal to the target.

So, we can say that initially, we need to find(n-1, target) which means that we are counting the number of subsequences in the array from index 0 to n-1, whose sum is equal to the target. Similarly, we can generalize it for any index ind as follows:

![](https://lh6.googleusercontent.com/Tg1yIUORXxkIz29VFcvKqlZoIkau7juWUUkmeBzUbR7Ir_ojbRefP-YDS854B1DcB3oxzgtyxJhodK2DjsgNU9H7d0KWJ9CTeOYuzRHdQM3GPt1Jq9ywanbT1qx4oaoB3_I0kDUc)

**Base Cases:**

- If target == 0, it means that we have already found the subsequence from the previous steps, so we can return 1.
- If ind== 0, it means we are at the first element, so we need to return arr[ind]== target. If the element is equal to the target we return 1 else we return 0.

![](https://lh6.googleusercontent.com/ZNA56C9DefUxAth8bkBBpGZ2VcYp5MB1jEjz1fkidtgpAeDTZxeQq5jPLU3nfR9Mot7fbmFcVtcAqo__HzA_bHvC_fcyhKSptlyos9zbSSQpASm5WFkZY_MaI-qrcEUqrEvEMNFW)

**Step 2:** Try out all possible choices at a given index.

We need to generate all the subsequences. We will use the pick/non-pick technique as discussed in this video “[Recursion on Subsequences](https://www.youtube.com/watch?v=AxNNVECce8c)”.

We have two choices:

- **Exclude the current element in the subsequence:** We first try to find a subsequence without considering the current index element. For this, we will make a recursive call to f(ind-1,target).
- **Include the current element in the subsequence:** We will try to find a subsequence by considering the current index as element as part of subsequence. As we have included arr[ind], the updated target which we need to find in the rest if the array will be target - arr[ind]. Therefore, we will call f(ind-1,target-arr[ind]).

**Note:** We will consider the current element in the subsequence only when the current element is less than or equal to the target.

![](https://lh5.googleusercontent.com/RZVIi-SEadz4ussGmd7HaRqOOg2e69n6dyhWglLJ5uf3iqK1_dv1rCCRugNOvRXb8wIZGRE2F9OgRoratgWZTB4x9heyVZAamEbG_L68Ufz7XJDeYOCU99BXEjvExoILeN4Yusrj)

**Step 3:  Return sum of taken and notTaken**

As we have to return the total count of subsets with the target sum, we will return the sum of taken and notTaken from our recursive call.

The final pseudocode after steps 1, 2, and 3:

![](https://lh4.googleusercontent.com/GXHrHVmcA-exoMgbh8Ur-xTaVslPJUD4CgFoAJnqfpFCM1eimvNd08Y8t8n8KWsRbTfssK3wFYBGxwFHQkRd_5ETixOKIHqNIS5kUVwuAfBZxRkBC-TRvk_wCiyXiqrdBVoU4gJ_)


#### Code - 
```C++
// Function to count partitions of the array into subsets with a given target sum
int countPartitionsUtil(int ind, int target, vector<int>& arr, vector<vector<int>>& dp) {
    // Base cases
    if (ind == 0) {
        if (target == 0 && arr[0] == 0)
            return 2; // Two ways to partition: include or exclude the element
        if (target == 0 || target == arr[0])
            return 1; // One way to partition: include or exclude the element
        return 0; // No way to partition
    }
    
    // If the result for this index and target sum is already calculated, return it
    if (dp[ind][target] != -1)
        return dp[ind][target];
        
    // Calculate the number of ways without taking the current element
    int notTaken = countPartitionsUtil(ind - 1, target, arr, dp);
    
    // Calculate the number of ways by taking the current element
    int taken = 0;
    if (arr[ind] <= target)
        taken = countPartitionsUtil(ind - 1, target - arr[ind], arr, dp);
        
    // Store the sum of ways in the DP array and return it
    return dp[ind][target] = (notTaken + taken);
}

// Function to count the number of ways to achieve the target sum
int targetSum(int n, int target, vector<int>& arr) {
    int totSum = 0;
    for (int i = 0; i < arr.size(); i++) {
        totSum += arr[i];
    }
    
    // Checking for edge cases
    if (totSum - target < 0)
        return 0; // Not possible to achieve the target sum
    if ((totSum - target) % 2 == 1)
        return 0; // The difference between the total sum and target sum must be even
    
    int s2 = (totSum - target) / 2; // Calculate the required sum for each subset
    
    vector<vector<int>> dp(n, vector<int>(s2 + 1, -1)); // Initialize DP table
    return countPartitionsUtil(n - 1, s2, arr, dp); // Call the helper function
}
```