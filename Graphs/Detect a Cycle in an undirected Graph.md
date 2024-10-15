  We do a standard DFS traversal, and if we visit a node twice, then it is a cycle,
  the modification is that to avoid using the visited array in its normal form, which will give every undirected edge as a cycle. 
  We go on every index of the adjacency list, then move to every other node that is not where we had come from originally, that is not go back to ur parent.
  Now we can keep the visited array and use it to detect the cycle.

input is in the form of adjacency list - `vector<int> gr[]`
nodes are from 1 to v

```C++
bool cycleInUndirectedGraph(int node, vector<int> gr[], vector<bool>& vis, int par){
	vis[node]=true;
	for(auto child:gr[node]){ //visit the node, go to all childs
		if(!vis[child])  //go to unvisited node 
		//wrap this in more if statement, based on question and done.
			if(cycleInUndirectedGraph(child, gr, vis, node))
				//if cycle is found inside, return true
				return true;
		else if(child!=par) return true; //visited, but not parent, cycle.
	}
	return false;
}

bool isCycle(int v, vectro<int> gr[]){
	vector<bool> vis(v);
	for(int node=0; node<v; node++)
	{
		if(!vis[node]) //to handle multiple components 
			if(cycleInUndirectedGraph(node, gr, vis, -1))
				return true;
	}
	return false;
}
```

O(V+E) -> time complexity

**Find Redundant Connection LeetCode -** 
[Redundant Connection - LeetCode](https://leetcode.com/problems/redundant-connection/description/)

```C++
class Solution {
public:
    bool dfs(int src, int parent, vector<int> adj[], vector<bool>& vis) {
        vis[src] = true;
        for (auto adjnode : adj[src]) {
            if (!vis[adjnode]) {
                if (dfs(adjnode, src, adj, vis))
                    return true;
            } else if (adjnode != parent)
                return true;
        }
        return false;
    }

    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        int n = edges.size();
        vector<int> adj[n + 1];
        for (int i = 0; i < n; i++) {
            adj[edges[i][0]].push_back(edges[i][1]);
            adj[edges[i][1]].push_back(edges[i][0]);
            vector<bool> vis(n + 1, false);
            if (dfs(edges[i][0], -1, adj, vis)) {
                return edges[i];
            }
        }
        return {};
    }
};
```



