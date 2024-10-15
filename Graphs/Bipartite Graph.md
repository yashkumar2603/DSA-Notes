colour the graph with 2 colors, and no 2 nodes must be same colour.
So odd length cycles cant be bipartite.
even length cycle and linear is always bipartite(basically everything except odd cycle)


We dont need to use a visited array, we can just use the color array and also use it as the visited.
If the color is something other than -1, the node is visited.
take colour 1 as 1 in array and colour 0 as 0 in array
```C++
//make a simple traversal and then start colouring in colours, if not possible anywhere,then return false.
bool bfs(int i, int v, vector<vector<int>>& gr, color)
{
	queue<int> q;
	q.push(i);
	color[i]=0;
	while(!q.empty())
	{
		int node = q.front();
		q.pop();
		for(auto it: gr[node]){
			if(color[it]==-1)
			{
				color[it]=!color[node];
				q.push(it);
			}
			else if(color[it]==color[node]) return false;
		}
	}
	return true;
}
bool isBipartite(int v, vector<vector<int>> gr)
{
	vector<int> color(v);
	for(int i=0; i<v; i++)
	{
		color[i]=-1;
	}
	for(int i=0; i<v; i++)
	{
		if(color[i]==-1)
		{
			if(bfs(i, v, gr, color)==false){
				return false;
			}
		}
	}
	return true;
}
```

## Using DFS - 
```C++
bool dfs(int node, int col, vector<int> color, vector<int> gr)
{
	color[node]=col;
	for(auto it:gr[node]){
		if(color[it]==-1)
		{
			if(dfs(it, !col, color, gr)==false)
				return false;
		}
		else if(color[it]==col)
			return false;
	}
	return true;
}

bool isBipartite(int v, vector<vector<int>> gr)
{
	vector<int> color(v);
	for(int i=0; i<v; i++)
	{
		color[i]=-1;
	}
	for(int i=0; i<v; i++)
	{
		if(color[i]==-1)
		{
			if(dfs(i, 0, color, gr)==false){
				return false;
			}
		}
	}
	return true;
}
```