Useful in situations  like when we change the index of an element in the array and then query on a range, even if we use prefix sum and all, still we wont be able to get below O(n) time. This may not be ideal for the large number of testcases scenario.
## point Update - 
To get to a point, we see that from a particular, node, which side is the point to be updated, for example if we have to update the value at a[3] then we move in the left side of the tree and then go the the leaf node and update the value there. Then we backtrack and reach the leaf node. from the updated leaf node.
This takes at max log(n) time and is hence quite fast.
Code -
```C++
void pointupdate(int ind, int low, int high, int node, int val){
	if(low==high){
		arr[low] += val; 
		seg[ind] += val;
	}
	else{
		int mid=(low+high)>>1;
		if(node<=mid && node>=low) pointUpdate(2*ind+1, low, mid, node, val);
		else pointUpdate(2*ind+2, mid+1, high, node, val);
		seg[ind] = seg[2*ind+1] + seg[2*ind+2];  //whatever ur desired condition is.
	}
}
```


