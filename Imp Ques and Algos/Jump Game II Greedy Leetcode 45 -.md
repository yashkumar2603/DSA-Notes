# Done
## Jump Game II -
We have to find the min. number of jumps to be made in this problem. 
In this, we go from the start and then we see the range of positions possible from any current position and then update 2 pointers according to that.
```C++
int jump(vector<int>& nums) {
        int n=nums.size();
        int l=0, r=0;
        int res = 0;
        while(r<n-1)
        {
            int farthest = 0;
            for(int i=l; i<=r; i++)
                farthest = max(farthest, i + nums[i]);
            l = r+1;
            r = farthest;
            res++;
        }
        return res;
    }
```

Basically the farthest is finding the farthest we can go from the current window between l and r. Then updates the window like that.