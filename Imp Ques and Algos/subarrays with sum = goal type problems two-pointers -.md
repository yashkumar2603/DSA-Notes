[Binary Subarrays With Sum - LeetCode](https://leetcode.com/problems/binary-subarrays-with-sum/)

https://www.youtube.com/watch?v=xvNwoz-ufXA

U can convert multiple types of problems to this, can also be done by dp, but that is overkill.
```C++
class Solution {
public:
    int numSubarraysWithSum(vector<int>& nums, int goal) {
        unordered_map<int, int> count;
        count[0] = 1; //cuz if curr_sum-goal =0 then the current sum is target.
        int curr_sum = 0;
        int total_subarrays = 0;

        for (int num : nums) {
            curr_sum += num;
            if (count.find(curr_sum - goal) != count.end()) {
                total_subarrays += count[curr_sum - goal];
            }
            count[curr_sum]++;
        }

        return total_subarrays;
    }
};
```