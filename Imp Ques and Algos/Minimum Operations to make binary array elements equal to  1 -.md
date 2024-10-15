https://leetcode.com/contest/biweekly-contest-133/problems/minimum-operations-to-make-binary-array-elements-equal-to-one-i/description/
# Done
## Three element flip allowed - 
```C++
class Solution {
public:
    int minOperations(vector<int>& nums) {
        int n = nums.size();
        int operations = 0;

        for (int i = 0; i <= n - 3; ++i) {
            if (nums[i] == 0) {
                // Flip nums[i], nums[i+1], nums[i+2]
                nums[i] = 1 - nums[i];
                nums[i + 1] = 1 - nums[i + 1];
                nums[i + 2] = 1 - nums[i + 2];
                operations++;
            }
        }

        // Check if all elements are 1
        for (int i = 0; i < n; ++i) {
            if (nums[i] == 0) {
                return -1; // It's impossible to make all elements 1
            }
        }

        return operations;
    }
};
```

## Flip from current to the end at once - 
```C++
class Solution {
public:
    int minOperations(vector<int>& nums) {
        int ans = 0;
        int current = 1; // Assuming we want to end up with all 1s
        
        for(int i = 0; i < nums.size(); i++) {
            if (nums[i] != current) {
                ans++;
                current = 1 - current; // Flip current expectation
            }
        }
        
        return ans;
    }
};
```

