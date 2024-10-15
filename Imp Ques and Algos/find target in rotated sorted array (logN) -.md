# Done 
```C++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int low = 0;
        int high = nums.size() - 1;
        
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[low] <= nums[mid]) {
                if (nums[low] <= target && target <= nums[mid]) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            } else {
                if (nums[mid] <= target && target <= nums[high]) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
        }
        
        return -1;
    }
};
```

Find minimum element - 
```C++
class Solution {
public:
    int findMin(vector<int>& nums) {
        int l=0; int r = nums.size()-1;
        while(l<r){
            int m=(l+r)/2;
            if(nums[m] < nums[r]){
                r=m;
            }
            else {
                l=m+1;
            }
        }
        return nums[l];
    }
};
```

