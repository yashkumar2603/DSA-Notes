Segment trees are used whenever we are asked queries for a range in any problem. 
we construct the tree with indexing, the root is indexed as 0 and the root holds the range value from 0-n.
The children each are indexed as 2* root index +1 (left) and 2* root index+2 (right). 
They hold the ranges from 0 to(0+n)/2 (left) and (0+n)/2 to n (right)
Max. number of nodes in segment tree is 4* n, so we use that when declaring the segment tree array.
![[Pasted image 20240511224220.png|900]]

## Filling and Usage -
To fill the segment tree, the exact numbers used for filling depend on the condition employed for the filling, for example, if the condition is maximum of a range -> we fill in the manner -
- when we have the range of 0, that is same numbers on both sides of the range, then fill with that index from the array.
- Then use the condition, for this question the maximum of the range, that is to fill the 0-1 range, we take max of 0-0 and 1-1 node and place it in the 0-1 node.
- similarly keep doing till the root, basically, the root is formed from the max of the two halves.

Now, due to the indexing given, we can store this up in an array. 
## Querying - 
The basic gist is that we follow three rules for the given query range - 
1. Stored range Lies completely inside one of the queried ranges - return the value.
2. Stored range does not lie at all in the queried range - return INT_MIN(as small as possible, as we have to find the max and this should not contribute to our answer).
3. Stored Range overlaps with queried range (partially lies inside and outside) - We go into both directions and query it, then according to the question, take the max of the values obtained from both the sides., the returns follow the above two rules.

This is how the querying works 
Time taken to build tree - O(n)
Time taken to query - O(logn) (height of the tree)

<font color="#f79646">Build Code - </font>
```C++
int a[100005]; int seg[4*100005]
void build(int ind, int low, int high){
	if(low==high){
		seg[ind]=a[low];
		return;
	}
	int mid=(low+high)/2;
	build(2*ind+1, low, mid);
	build(2*ind+2, mid, high);
	//now backtrack and fill values
	seg[ind] = max(seg[2*ind+1], seg[2*ind+2]);  //for maximum, calculate whatever needed.
}
```

for building, call `build(0,0,n-1)`

<font color="#f79646">Query code -</font>
```C++
int query(int ind, int low, int high, int l, int r){
	if(low>=l && high<=r)
		return seg[ind];
	if(high<l || low>r) return INT_MIN; //for storing maximums, return whatever suits the problem.
	int mid = (lo+high)/2;
	int left = query(2*ind+1, low, mid, l, r);
	int right = query(2*ind+2, mid+1, high, l, r);
	return max(left, right); //Or whatever suits the problem.
}
```

For example, for sum just replace max by addition of the two values.

[[Segment Trees Point and Range Updates -]]
