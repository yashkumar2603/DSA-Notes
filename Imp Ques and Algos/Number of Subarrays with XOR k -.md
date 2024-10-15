# Done
[[XOR -]]
[(317) Number of Subarrays with xor K | Brute - Better - Optimal - YouTube](https://www.youtube.com/watch?v=eZr-6p0B7ME)
Given an array, find the number of subarrays with XOR  = k.
The brute force solution is to use 2 loops and then keep a XOR variable, continue taking XOR and check at each step and have a counter as the answer.

<font color="#f79646">Optimal Approach -</font> 
For the optimal approach we have to see that for the XOR of m continuous elements from the array to be k, given that the XOR of all the n elements of the array is XR.
W have to have another subarray of (n-m) elements whose XOR is XR^k. 
Now, using this we can move backwards in the manner that if there is a subarray ending at index i having a XOR of k, then there must be a subarray from the start with XOR = XR^k, where XR is the XOR from the front to index i(stored in a prefix XOR array).

<font color="#f79646">Implementation - </font>
Using Hashmap, 
What we do is we take a hashmap with initially 0 mapped to 1 (as XOR 0 occurs once, when we choose an empty subarray). 
Then we move ahead and Take XOR with next element and check is the XOR^k was seen before, if yes we add the no. of times it was seen before to the answer. If not seen, we simply add the current XOR to the hashmap and move ahead repeating the same thing.
```C++
int subarraysWithXorK(vector<int> a, int k) {
    int n = a.size(); //size of the given array.
    int xr = 0;
    map<int, int> mpp; //declaring the map.
    mpp[xr]++; //setting the value of 0.
    int cnt = 0;

    for (int i = 0; i < n; i++) {
        // prefix XOR till index i:
        xr = xr ^ a[i];

        //By formula: x = xr^k:
        int x = xr ^ k;

        // add the occurrence of xr^k
        // to the count:
        cnt += mpp[x];

        // Insert the prefix xor till index i
        // into the map:
        mpp[xr]++;
    }
    return cnt;
}
```

Similar Questions - 
[XOR Queries of a Subarray - LeetCode](https://leetcode.com/problems/xor-queries-of-a-subarray/description/)
In this, to evaluate the XOR of a given range, we can just take the XOR till the end and XOR it with the XOR till before the start and then return that.
