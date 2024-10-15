https://leetcode.com/problems/special-array-with-x-elements-greater-than-or-equal-x/description/?envType=daily-question&envId=2024-05-27

<iframe width="560" height="315" src="https://www.youtube.com/embed/NqupGY4-1tQ?si=XtXZBrCdpaD1JtjK" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
Quite tricky, watch the video. 
basically, the max we have to check is upto n, the size of the input array. As there cant be n+1 numbers greater than n+1 in the array as there aren't n+1 elements in the first place. 
So we create an array of length n, and then store the number of elements greater than i in the array 1<i< n . But, all elements greater than n are counted at the nth index only.
![[Pasted image 20240527165805.png|425]]


Code - 
```C++
class Solution {
public:
    int specialArray(vector<int>& nums) {
        int n= nums.size();
        int s=0;
        vector<int> cnt(n+1, 0);
        for(int i=0; i<n; i++) 
        {
            cnt[min(nums[i], n)]++;
        }
        for(int i=n; i>=1; i--)
        {
            s+=cnt[i];
            if(s==i) return i;
        }
        return -1;
    }
};
```

