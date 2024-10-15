# Done
# 
Unique problem
https://leetcode.com/problems/gas-station/
We subtract the gas from the cost and then loop around in the subtracted array, then try starting from each index and keep summing elements from this array, checking if we can loop around, at any point, if the gas in tank goes negative, we cant do the loop starting from that index. ->brute force, the solution is optimized by using greedy, but this is a very unique problem, so memorize the solution.
```C++
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        if (accumulate(gas.begin(), gas.end(), 0) < accumulate(cost.begin(), cost.end(), 0)) {
            return -1;
        }

        int total = 0;
        int res = 0;
        for (int i = 0; i < gas.size(); i++) {
            total += (gas[i] - cost[i]);

            if (total < 0) {
                total = 0;
                res = i + 1;
            }
        }
        return res;
    }
};
```

