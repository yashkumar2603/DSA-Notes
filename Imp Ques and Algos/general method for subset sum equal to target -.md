# Done
```C++
f(ind, target)
{
	if(target==0) return true;
	if(ind==0) return arr[0]==target;
	
	nottake = f(ind-1, target);
	
	take=false;
	if(arr[ind]<=target)
		take = f(ind-1, target-arrr[ind]);
	
	return take|nottake;
}
```





