# Done
The brute force approach is to just generate all the fractions, and then sorting them and getting the kth smallest prime fraction. 
But this is $O(n^2 \times log(n^2))$ time complexity.
We need to do much better than this. 
So we see another solution -
We have to make sure to use the property given that the given array is a sorted array and has only 1 and prime numbers in it.
we can use a priority queue to boost it by taking the factor that the array is sorted.

# Approach

1. Initialization: Start by initializing a priority queue (pq) to store pairs of fractions (x, {numerator, denominator}), where x represents the value of the fraction (numerator divided by denominator).
2. Pair Generation: Iterate through the array arr, considering every pair of elements (arr[i], arr[j]) where i < j. Calculate the fraction x = arr[i] / arr[j] as a double.
3. Priority Queue Management:  
    If the size of the priority queue reaches k, check if the current fraction x is smaller than the top fraction in the queue. If it is, pop the top element and push the current fraction into the queue.  
    If the size of the priority queue is less than k, simply push the current fraction into the queue.
4. Result Extraction: After processing all possible pairs, the top element of the priority queue will contain the kth smallest prime fraction. Extract the numerator and denominator from this element and return them as the result.

# Complexity

- Time complexity: O(n^2 * log(k))

- Space complexity: O(k)

# Code

```cpp
class Solution {
public:
    vector<int> kthSmallestPrimeFraction(vector<int>& arr, int k) {
        int n = arr.size();
        priority_queue<pair<double,pair<int,int>>> pq;

        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                double x = arr[i]/(arr[j]*1.0);
                
                if(pq.size() == k){
                    if(x < pq.top().first){
                        pq.pop();
                        pq.push({x,{arr[i],arr[j]}});
                    }
                }
                else{
                    pq.push({x,{arr[i],arr[j]}});
                }
            }
        }

        return {pq.top().second.first,pq.top().second.second};
    }
};
```

 