# Done

```C++
class Solution {
public:
    bool isok(vector<int>& weights, int days, int capacity) {
        int curr = 0;
        int curr_days = 1;
        for (int weight : weights) {
            if (curr + weight > capacity) {
                curr_days++;
                curr = 0;
            }
            curr += weight;
            if (curr_days > days) {
                return false;
            }
        }
        return true;
    }

    int shipWithinDays(vector<int>& weights, int days) {
        //binary search template
        int hi=accumulate(weights.begin(), weights.end(), 0);
        int lo=*max_element(weights.begin(), weights.end());
        int mid;
        while(lo<hi)
        {
            mid=(hi+lo)/2;
            if(isok(weights, days, mid))
            {
                hi=mid;
            }
            else{
                lo=mid+1;
            }
        }
        return lo;
    }
};
```

