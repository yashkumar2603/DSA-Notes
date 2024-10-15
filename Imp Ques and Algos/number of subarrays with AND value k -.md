[Number of Subarrays With AND Value of K - LeetCode](https://leetcode.com/problems/number-of-subarrays-with-and-value-of-k/description/)
Initialization:

`c` is initialized to 0 to keep track of the count of subarrays whose bitwise AND is equal to k.  
`feasible` is a set that will store all unique bitwise AND results of subarrays ending at the current position.  
`pmp` is a map that will store the count of subarrays ending at the current position with their bitwise AND results.  
n is the size of the input array nums.  
Loop through the Array:

For each element `nums[i]` in the array, a new set `new_feasible` and a new map mp are created to store the bitwise AND results and their counts for subarrays ending at i.  
Update for the Current Element:

Insert `nums[i]` into `new_feasible` since the subarray [`nums[i]`] (a single element) has a bitwise AND of `nums[i]`.  
Increment the count of `nums[i]` in mp.  
Update for Existing Feasible Subarrays:

For each element j in the `feasible` set (which represents unique bitwise AND results of subarrays ending at previous positions), calculate the bitwise AND of j with `nums[i]` and insert the result into `new_feasible`.  
Update the count of this result in `mp` by adding the count of j from `pmp`.  
Count Subarrays with AND Equal to k:

Add the count of subarrays ending at i with a bitwise AND equal to k (if any) to `c`.  
Update for the Next Iteration:

Set `pmp` to `mp` for the next iteration.  
Set `feasible` to `new_feasible` for the next iteration.

# Complexity

- Time complexity:  
    O(30∗n)
    
- Space complexity:  
    O(1)

```C++
class Solution {
public:
    long long countSubarrays(vector<int>& nums, int k) {
        long long c=0;
       set<int>feasible;
        int n=nums.size();
        map<int,int>pmp;

        for(int i=0;i<n;i++)
        {
             set<int>new_feasible;
              map<int,int>mp;
                 new_feasible.insert(nums[i]);
           mp[nums[i]]++;
            for(auto j:feasible)
            {
                 new_feasible.insert(nums[i]&j);
                mp[nums[i]&j]+=pmp[j];
            }
             
            c+=mp[k];
            pmp=mp;
            

            feasible=new_feasible;
        }
        return c;
        
    }
};

```

**another solution -** 
# Intuition

- For a subarray A[l..r] if AND is X then for all subarray of this subarray has an AND Y where Y>=X.
    
- Adding a number will cause decrease or unchange of AND.
    
- Removing a number will cause increase or unchange of AND.
    

# Approach

- AtLeastK(nums, k) -> will return number of subarray which has an AND atleast k
- `Ans = AtLeast(k) - AtLest(k+1)`

# Complexity

- Time complexity: O(32∗n)

- Space complexity: O(1) Frequency vector of size 32.
```C++

class Solution
{
public:
    long long countSubarrays(vector<int> &nums, int k)
    {
        return atLeastK(nums, k) - atLeastK(nums, k + 1);
    }
    long long atLeastK(vector<int>& nums, int k){
        long long ans = 0;
        vector<int> temp(32, 0);
        int l = 0;
        for (int r = 0; r < nums.size(); r++)
        {
            for (int i = 0; i < 32; i++)
            {
                if ((1 << i) & nums[r])
                {
                    temp[i]++;
                }
            }
            while ((r - l + 1) > 0 && calc(temp, r - l + 1) < k)
            {
                for (int i = 0; i < 32; i++)
                {
                    if ((1 << i) & nums[l])
                    {
                        temp[i]--;
                    }
                }
                l++;
            }
            ans += (r - l + 1);
        }
        return ans;
    }

    //function to calculate the AND from frequency vector
    int calc(vector<int>& temp, int w){
        int ans = 0;
        for (int i = 0; i < 32;i++){
            if(temp[i]==w)
                ans += (1 << i);
        }

        return ans;
    }
};
```

