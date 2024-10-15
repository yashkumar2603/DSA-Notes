[CSES - Meet in the Middle](https://cses.fi/problemset/task/1628)
[Partition Array Into Two Arrays to Minimize Sum Difference - LeetCode](https://leetcode.com/problems/partition-array-into-two-arrays-to-minimize-sum-difference/description/)

Both are on the same concept
Another problem is the Apple division problem -> [[CSES Problem set Notes -]]

## Approach -

### CSES Problem - 
We have the constraints as $1<n<40$, so we have to use something better than $n \times 2^n$ brute force as $40 \times 2^{40}$ wont pass. The max Acceptable time is $2^{28}$ .
So we make the observation that we dont have to search on the whole array, we can generate for half the array, it is $2^{20}$ acceptable. So. we do for the 2 halves.
We will have to have the sums of the elements. We will now go thru the sums in the left hand side and then try to find target(which is sum/2)-leftSum in the right side of the map in which we stored all this. and this is how it is done.
