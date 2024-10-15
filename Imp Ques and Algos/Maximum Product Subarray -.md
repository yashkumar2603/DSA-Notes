[Max Product Subarray | Interviewbit](https://www.interviewbit.com/problems/max-product-subarray/)
```C++
int Solution::maxProduct(const vector<int> &A) {
    int pre=1, suff=1;
    int ans=INT_MIN;
    int n=A.size();
    for(int i=0; i<A.size(); i++){
        if(pre==0){pre=1;}
        if(suff==0){suff=1;}
        
        pre = pre*A[i];
        suff=suff*A[n-i-1];
        ans=max(ans, max(pre, suff));
    }
    return ans;
}

```
