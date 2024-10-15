VERY INGENIOUS QUESTION
# Done, But Left for later
[1438. Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit](https://leetcode.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit/)
**Solution**
https://youtu.be/LDFZm4iB7tA?si=PPeDMCpaLXWYZKZz

```C++
class Solution {
public:
    int longestSubarray(vector<int>& nums, int l) {
        int ans=0,n=nums.size();
        deque<int> dqmin, dqmax; 
        int j=0;
        for(int i=0;i<nums.size();i++)
        {
            //if one bigger element arrives in window then smaller element will will never appear in picture of maximum elements.
            while(dqmax.size() && dqmax.back()<nums[i]) dqmax.pop_back();
            //if one small element arrives in window then bigger element will will never appear in picture of minimum elements.
            while(dqmin.size() && dqmin.back()>nums[i]) dqmin.pop_back();
            
            dqmin.push_back(nums[i]);  dqmax.push_back(nums[i]);

            int maxi=dqmax.front(), mini=dqmin.front();
            if(maxi-mini<=l) ans=max(i-j+1,ans);
            else // if diff is greater then limit then we have to pop to end
            {
                if(nums[j]==dqmax.front()) dqmax.pop_front();
                if(nums[j]==dqmin.front()) dqmin.pop_front();
                j++;
            }
        } 
        return ans;
    }
};
```