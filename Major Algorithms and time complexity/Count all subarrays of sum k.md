# done
take the array, iterate on it, maintain a hashmap of already seen prefix sums and map it to their count, take an integer for the current sum. and go on iterating on the array and finding out the prefix sum each time. and adding to the hashmap. also check that if the `current_sum - goal` is present or not, if present then increment the answer by the number of times it has been seen before(this is done because if it has been spotted now and also before, then we can use the previous combination subtracted from the current one too).
```C++
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
```
[Count Subarray sum Equals K | Brute - Better -Optimal (youtube.com)](https://www.youtube.com/watch?v=xvNwoz-ufXA)
# Watch this video (beautiful logic, imp for CP)