balanced is when the difference between the height of left and right subtree is at max 1.
That is the difference is either 0 or  1.

To do this, we use the code used to find the height of the tree in O(n).
```C++
int check(node){ //find height in O(N)
	if(node==NULL)
		return 0;
	lh=check(node->left);
	rh=check(node->right);
	return max(lh, rh)+1;
}
```

Modify this -
```C++
int check(node){ //find height in O(N)
	if(node==NULL)
		return 0;
	lh=check(node->left);
	rh=check(node->right);
	if(lh==-1 || rh==-1) return -1;
	if(abs(lh-rh)>1) return -1;
	return max(lh, rh)+1;
}
```

Now check in main if the return is anything but -1, tree is balanced
otherwise not.