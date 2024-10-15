**asked directly in OA and Interviews so  study, but do via BFS in problems**

Since DFS goes to the depth first, so we add while returning back and only when all the children are completed.
So we take a visited array 

```C++
void dfs(int node, vector<int>& tSort, vector<bool>& vis, vector<vector<int>>& gr)
{
	vis[node]=true;
	for(auto ne:gr[node]){
		if(vis[ne]==false)
			dfs(ne, tSort, vis, gr);
	}
	tSort.push_back(node); //push_back while returning
}

vector<int> topoSort(int V, vector<vector<int>> gr)
{
	vector<bool> vis(V,0);
	vector<int> tSort;
	for(int node=0; node<V; node++)
	{
		if(vis[node]==false)
		{
			dfs(node, tSort, vis, gr);
		}
	}
	reverse(tSort.begin(), tSort.end());
	return tSort;
}
```

