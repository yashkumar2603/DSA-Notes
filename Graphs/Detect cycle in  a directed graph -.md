pIn this, we cannot use the same visited array technique, as the visits might happen from different paths and then get detected as visited and a false cycle.
Only visited in same path must be marked to form a cycle.

So we will take 2 vectors, a visited and a path visited.
On moving, we add to visited and path visited, if it is a dead end, we come back and while coming back, we remove the nodes of that path from path visited.
Then go again in different path, if visited is marked, we dont go there. But if visited and path visited both are marked, we have found a cycle.

```C++
bool cycleInUndirectedGraph(int node, vector<vector<int>> gr, vector<bool>& visited, vector<bool>& pathVisited))
{
	visited[node]=true;
	pathVisited[node]=true;

	for(auto child : gr[node]){
		if(!visited[child]){
			if(cycleInUndirectedGraph(child, gr, visited, pathVisited)) //child found the cycle
				return true;
		}
		else if(pathVisited[child]==true){
			return true; //visited and path visited
		}
	}
	pathVisited[node] = false; //moving back so deleting path visited
	return false;
}

bool isCyclic(int v, vector<vector<int>> gr)
{
	vector<bool> visited(v,false);
	vector<bool> p_visited(v,false);
	for(int i=0; i<v; i++){
		if(visited[i]==false)
			if(cycleInUndirectedGraph(i, gr, visited, pathVisited))
				return true;
	}
	return false;
}
```

