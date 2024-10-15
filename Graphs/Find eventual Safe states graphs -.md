### BFS Way (with topo sort) - 
We take the graph, we then reverse each node, then we apply a half topo sort, basically we take the vertices with 0 indegree and push into the queue and decrease the indegree of the connected nodes to it by 1 and pop the queue(standard topo sort thing)
we push in the indegree 0 elements into our queue and push all the elements that are popped from the queue into our answer array.
The final array we get is actually the eventual safe nodes, now sort it and return.

```C++
class Solution {
public:
    vector<int> eventualSafeNodes(vector<vector<int>>& graph) {
        //adjacency list given
        int n=graph.size();
        vector<vector<int>> revgr(n);
        vector<int> indegree(n);
        for(int i=0; i<n; i++)
        {
            for(auto ne:graph[i])
            {
                revgr[ne].push_back(i);
                indegree[i]++;
            }
        }
        queue<int> q;
        vector<int> ans;
        for(int i=0; i<n; i++)
        {
            if(indegree[i]==0)
            {
                q.push(i);
            }
        }
        while(!q.empty())
        {
            int node=q.front();
            q.pop();
            ans.push_back(node);

            for(auto it:revgr[node])
            {
                indegree[it]--;
                if(indegree[it]==0) q.push(it);
            }
        }
        sort(ans.begin(), ans.end());
        return ans;
    }
};
```

### Using DFS - 
Less space complexity (no reverse graph adjacency list here)
We will use the cycle detection in directed graph algo here.
The idea is, if u dry run, we will see that every vertex that is a part of a cycle or is pointing into a cycle is not a safe node, so we just need to eliminate the nodes that are in cycle or pointing into one of the members of the cyclic nodes.
We do our standard bfs and if all the paths from one node end up at a safe node, (indegree=0) we put it in ans
while returning back as well, we need t obe be careful of this.
```C++
class Solution {
private:
	bool dfsCheck(int node, vector<int> adj[], int vis[], int pathVis[], int check[]) {
		vis[node] = 1;
		pathVis[node] = 1;
		check[node] = 0;
		// traverse for adjacent nodes
		for (auto it : adj[node]) {
			// when the node is not visited
			if (!vis[it]) {
			if (dfsCheck(it, adj, vis, pathVis, check) == true) {
					check[node] = 0;
					return true;
				}

			}
			// if the node has been previously visited
			// but it has to be visited on the same path
			else if (pathVis[it]) {
				check[node] = 0;
				return true;
			}
		}
		check[node] = 1;
		pathVis[node] = 0;
		return false;
	}
public:
	vector<int> eventualSafeNodes(int V, vector<int> adj[]) {
		int vis[V] = {0};
		int pathVis[V] = {0};
		int check[V] = {0};
		vector<int> safeNodes;
		for (int i = 0; i < V; i++) {
			if (!vis[i]) {
				dfsCheck(i, adj, vis, pathVis, check);
			}
		}
		for (int i = 0; i < V; i++) {
			if (check[i] == 1) safeNodes.push_back(i);
		}
		return safeNodes;
	}
};
```

