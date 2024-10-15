# Done
In the algorithm, we keep on adding elements to our value of sum and maintain a an ans initially set to INT_MIN. 
We iterate and add elements to the sum variable and check everytime if the current sum<0, if it is then sum=0. and then check if sum>ans, if it is, then ans=sum.
```C++
int maxSubArray(vector<int>& nums) {
        int curr = nums[0];
        int result = nums[0];
        
        for (int i = 1; i < nums.size(); i++) {
            curr = max(curr + nums[i], nums[i]);
            result = max(result, curr);
        }
        
        return result;
        return max(0, result); //if empty subarray is considered.
    }

/* this is important in the case where 
a=[-4,-1,-2,-1] for example
Then, the answer will be -1, but if we take an empty subarray the sum is 0 which is greater. so it depends in the requirements.
*/
```

### Now to find the exact subarray for which the maximum sum was found - 
The key idea is that whenever we have the current sum = 0 we are starting to build the subarray. and then when ans== sum, we are ending the subarray.
Se we define 3 new values, ansStart, ansEnd, start.
new modified code -
```C++
int ans=INT_MIN;
int sum = 0;
int start;
int ansStart=-1, ansEnd=-1;
for(int i=0; i<n; i++)
{
	if(sum==0) start=i;
	sum+=a[i];
	sum=max(0, sum);
	ans=max(ans, sum);
	if(ans==sum) {ansStart=start; ansEnd=i;}
}
cout<<ans<<nl; //if emptysubarray not considered
cout<<max(0,ans)<<nl; //if empty subarray considered.

//print the subarray running loop from ansStart to ansEnd.
```

