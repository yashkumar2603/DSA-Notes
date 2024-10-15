```C++
int dfs(int src, vector<int>& vis, vector<vector<int>>& gr, vector<int> subSize)
{
//subSize stores the size of each subtree of each src node.
	vis[src]=1;
	int curSize=1;
	for(auto child : gr[src]){
		if(vis[child]==0) 
			curSize += dfs(child, vis, gr, subSize);
	}
	return subSize[src] = curSize;
}
```

