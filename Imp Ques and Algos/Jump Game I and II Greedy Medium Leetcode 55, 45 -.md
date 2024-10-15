# Done
# Intuition

Think in a top-down approach, remember we are only asked if it is possible or not, not the min. number of moves or the exact moves. So this gives us a lot of freedom.

# Approach

Assume we reached the final position, then we need to back draft from there and try to reach the second last or further backward position. So we now have our new goal to reach the position somewhere behind.
Now, this happens only if the value of current position + the max. allowed jump>=the current goal. If this happens then we shift the goal to the current position. On doing this if we reach the index 0. It is possible to reach the end by following the constraints.

# Complexity

- Time complexity : O(n)

# Code

```cpp
class Solution {
    // we reach the end, then we have to figure out how to reach the previous one. Then recurse.
public:
    bool canJump(vector<int>& nums) {
        int n = nums.size();
        int goal = n-1;
        for(int i = n-1; i>=0; i--)
        {
            if(i + nums[i]>=goal) goal=i;
        }
        if(goal == 0) return true;
        return false;
    }
};
```

