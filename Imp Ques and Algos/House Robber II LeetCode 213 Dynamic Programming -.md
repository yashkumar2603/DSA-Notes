[House Robber II - LeetCode](https://leetcode.com/problems/house-robber-ii/)
# done
```C++
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        // Edge cases
        if (n == 1) return nums[0];
        else if (n == 2) return max(nums[0], nums[1]);

        // First, consider the case where we rob the first house (house 0)
        int a = 0, b = 0, c = 0;
        for (int i = n - 2; i >= 2; i--) {
            if (i == n-2) a = nums[i]; // Base case: Only one house to rob
            else if (i == n-3) a = max(nums[i], nums[i+1]); // Base case: Two houses to rob
            else a = max(nums[i]+c, b);
            c = b; b = a;
        }

        // Then, consider the case where we don't rob the first house.
        int a1 = 0, b1 = 0, c1 = 0;
        // We use dynamic programming to find the maximum sum of non-adjacent houses.
        for (int i = n - 1; i >= 1; i--) {
            if (i == n-1) a1 = nums[i]; // Base case: Only one house to rob
            else if (i == n-2) a1 = max(nums[i], nums[i+1]); // Base case: Two houses to rob
            else a1 = max(nums[i]+c1, b1);
            c1 = b1; b1 = a1;
        }

        // The result is the maximum sum of non-adjacent houses among the two cases.
        return max(nums[0]+a, a1);
    }
};
```