N nodes, N-1 edges and each of the nodes are reachable from one another.

## Prim's Algorithm - 

```C++
//Function to find sum of weights of edges of the Minimum Spanning Tree.
	int spanningTree(int V, vector<vector<int>> adj[])
	{
		priority_queue<pair<int, int>,
		               vector<pair<int, int> >, greater<pair<int, int>>> pq;
		vector<int> vis(V, 0);
		// {wt, node}
		pq.push({0, 0});
		int sum = 0;
		while (!pq.empty()) {
			auto it = pq.top();
			pq.pop();
			int node = it.second;
			int wt = it.first;

			if (vis[node] == 1) continue; //already visited, dont do anything
			// add it to the mst
			vis[node] = 1; //mark visited after popping, not while pushing
			sum += wt;
			for (auto it : adj[node]) {
				int adjNode = it[0];
				int edW = it[1];
				if (!vis[adjNode]) {
					pq.push({edW, adjNode});
				}
			}
		}
		return sum;
	}
```

##### To also store the MST edges we need to carry the parent in each step - 
```C++
int spanningTree(int V, vector<vector<int>> adj[]) {
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    vector<vector<int>> mstEdges;
    vector<int> vis(V, 0);
    vector<int> parent(V, -1);  // To store the parent of each node
    mstEdges.clear();  // Clear the MST edges vector
    pq.push({0, 0});  // {weight, node}
    int sum = 0;
    
    while (!pq.empty()) {
        auto it = pq.top();
        pq.pop();
        int node = it.second;
        int wt = it.first;
        
        if (vis[node] == 1) continue;
        
        // Mark the node as visited and add its weight to the sum
        vis[node] = 1;
        sum += wt;
        
        // If the node has a parent, add the edge to the MST edges
        if (parent[node] != -1) {
            mstEdges.push_back({parent[node], node, wt});
        }
        
        // Explore the adjacent nodes
        for (auto adjNodeInfo : adj[node]) {
            int adjNode = adjNodeInfo[0];
            int edW = adjNodeInfo[1];
            if (!vis[adjNode]) {
                pq.push({edW, adjNode});
                parent[adjNode] = node;  // Set the parent of the adjacent node
            }
        }
    }
    return sum;
}
```




