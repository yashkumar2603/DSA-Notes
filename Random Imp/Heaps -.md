**kth Largest Integer in a data stream -** 
https://leetcode.com/problems/kth-largest-element-in-a-stream/
keep the min_heap of size k and keep popping if more than k elements, as we only need the top k largest elements.
```C++
class KthLargest {
public:
    priority_queue<int, vector<int>, greater<int>> pq;
    int k;
    KthLargest(int k, vector<int>& nums) {
        this->k = k;
        int n=nums.size();
        for(int i=0; i<n; i++)
        {
            pq.push(nums[i]);
            if(pq.size()>k) pq.pop();
        }
    }
    
    int add(int val) {
        pq.push(val);
        while(pq.size()>k) pq.pop();
        return pq.top();
    }
};
```


