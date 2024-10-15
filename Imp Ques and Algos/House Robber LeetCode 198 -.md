# Done
[House Robber - LeetCode](https://leetcode.com/problems/house-robber/)

- The loop iterates through each house in the `nums` vector.
- For each house `i`, the algorithm calculates the maximum amount of money that can be robbed if the current house is included. This is done by taking the maximum of two options:
    - Robbing the current house `i` and adding its money (`nums[i]`) to the maximum amount of money that can be robbed from the houses up to the house `i-2` (which is stored in `pre`).
    - Not robbing the current house `i`, in which case the maximum amount of money that can be robbed remains the same as the previous house (stored in `cur`).
- `temp` stores this maximum value.
- `pre` is then updated to the value of `cur` (to move the window forward).
- `cur` is updated to the value of `temp` (to include the current house).
```C++
class Solution {
public: 
    int rob(vector<int>& nums) {
        int n = nums.size(), pre = 0, cur = 0;
        for (int i = 0; i < n; i++) {
            int temp = max(pre + nums[i], cur);
            pre = cur;
            cur = temp;
        }
        return cur;
    }
};
```