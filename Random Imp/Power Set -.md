```C++
int m=(1<<n);
for(int i=0; i<m; i++)
{
	for(int j=0; j<n; j++)
	{
		if(i & (1<<j))
			cout<<arr[i];
	}
	cout<<endl;
}
```

