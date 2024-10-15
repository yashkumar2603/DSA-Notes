Graph needs to be directed acyclic to be able to be topo-sorted.
In this, arrange the nodes such that all the edges of the directed graph point in one direction. 
Or like the ordering is such that every node is preceded by their dependency.
to effectively write it, arrange the elements in the graph such that the leftmost elements are those having no incoming nodes(no dependencies) and the rightmost have  no outgoing nodes, only dependencies. 
Then make levels according to distance in number of edges from the left side. Then write down each level separately and connect them up to make it topo-sorted.
The number of topo-sorts possible can be more than one as every level (imagine as a bucket can be shuffled in any way) its just that the order of the buckets must be correct. So the thing is that we need to make the least dependent ones leftmost and the most dependent ones rightmost.

Now, since we are writing down level wise, it is basically bfs traversal. (also solved by dfs but worse in intuition) 
BFS Topological sort code - 

For BFS we need the starting node, the starting nodes will be found based on the incoming degree of a node. the ones with in-degree=0 are the starting nodes
check in adjacency list, which of the nodes are not mentioned in any children of any node.

The main difference between bfs and topo-sort is that in bfs we push in the current node's children first and then pop the same level node, but in topo-sort we need to first pop out all of the current level, then only push. (resolve all dependencies before taking on the next level) This is so because, some edges would be skipping levels, so to avoid pushing a jumped level, we first push all the current level then move to next.

```C++
vector<int> toposort(int V, vector<vector<int>> gr){
	vector<int> indegree(V,0);
	for(int node=0; node<V; node++)  //get indegree of every node from the adjacency list
	{
		for(auto ne:gr[node]){
			indegree[ne]++;
		}
	}

	queue<int> q;
	for(int node=0; node<V; node++){  //push elements with indegree =0
		if(indegree[node]==0)
			q.push(node);
	}

	vector<int> tSort;
	while(!q.empty()){
		int sz=q.size();
		while(sz--){
			int node=q.front();
			q.pop();

			tSort.push_back(node);

			for(auto ne:gr[node]){  //as the parent is gone(popped) so in-degree reduces by 1, if indegree becomes 0, new start.
				indegree[ne]--;
				if(indegree[ne]==0)
					q.push(ne);
			}
		}
	}
	return tSort;
}
```
