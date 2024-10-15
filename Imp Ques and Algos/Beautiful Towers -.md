https://leetcode.com/problems/beautiful-towers-ii/description/
https://www.youtube.com/watch?v=qoJTmhtRV8I
 
**Very hard and good question on monotonic stack and prefix sum.**
```C++
class Solution {
public:
    long long maximumSumOfHeights(vector<int>& maxHeights) {
        int n=maxHeights.size();
        // calculating prefix sum;
        stack<int> s;
        vector<int> prevSmaller(n,-1);
        for(int i=0;i<n;i++){
            while(!s.empty()&&maxHeights[s.top()]>=maxHeights[i]){
                s.pop();
            }
            if(!s.empty()) prevSmaller[i]=s.top();
            s.push(i);
        }
        vector<long long> preSum(n);
        for(int i=0;i<n;i++){
            if(prevSmaller[i]==-1){
                preSum[i]=(long long)maxHeights[i]*(i+1);
            }
            else{
                preSum[i]=(long long)maxHeights[i]*(i-prevSmaller[i])+preSum[prevSmaller[i]];
            }
        }
        // calculating the suffix sum
        vector<int> nextSmaller(n,-1);
        s=stack<int>();
        for(int i=n-1;i>=0;i--){
            while(!s.empty()&&maxHeights[s.top()]>=maxHeights[i]) s.pop();
            if(!s.empty()) nextSmaller[i]=s.top();
            s.push(i);
        }
        vector<long long> SuffixSum(n);
        for(int i=n-1;i>=0;i--){
            if(nextSmaller[i]==-1){
                SuffixSum[i]=(long long)maxHeights[i]*(n-i);
            }
            else{
                SuffixSum[i]=(long long)maxHeights[i]*(nextSmaller[i]-i)+SuffixSum[nextSmaller[i]];
            }
        }
        // calculating the overall sum
        long long result=0;
        for(int i=0;i<n;i++){
            result=max(preSum[i]+SuffixSum[i]-maxHeights[i],result);
        }
        return result;
    }
};
```

