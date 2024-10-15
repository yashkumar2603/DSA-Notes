On weighted Undirected graph
Unapplicable to graphs with negative weights(it causes infinite loop on the negative weight edge)

Take a priority queue, push in the source and its distance(0).
the order in the pq is (dist, node), we need to keep min distance on the top.
now keep on going to the children of the top of the pq and if the dist(parent)+weight<distance(child) update it to the new small value, and push tha child in the pq only if the distance is updated, otherwise not.
TC - ElogV

If edges are weighted - Dijkstra uses Priority Queue/set DS
If edges are unweighted - Dijkstra uses Queue simply

#### Using Priority Queue - 
Queue is not used, because the queue doesnt arrange in priority order and so we end up considering worse paths as well and that too again and again.
```C++
vector<int> dijkstra(int V, vector<vector<vector<int>>> adj, int S)
{
	priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
	vector<int> dist(V);
	for(int i=0; i<V; i++)
	{
		dist[i]=INT_MAX;
	}
	dist[S]=0;
	pq.push({0,S});
	while(!pq.empty())
	{
		int dis = pq.top().first;
		int node = pq.top().second;
		pq.pop();

		for(auto it:adj[node])
		{
			int edgeWeight = it[1];
			int adjNode = it[0];

			if(dis+edgeWeight<dist[adjNode]){
				dist[adjNode] = dis+edgeWeight;
				pq.push({dist[adjNode], adjNode});
			}
		}
	}
	return dist;
}
```


#### Using Set DS (most Optimal) - 
Set is also ordered in the ascending order, so works better, and is faster than priority queue.
Set is used to erase already existing paths of higher cost
```C++
vector <int> dijkstra(int V, vector<vector<int>> adj[], int S)
    {
        // Create a set ds for storing the nodes as a pair {dist,node}
        // where dist is the distance from source to the node.
        // set stores the nodes in ascending order of the distances 
        set<pair<int,int>> st; 

        // Initialising dist list with a large number to
        // indicate the nodes are unvisited initially.
        // This list contains distance from source to the nodes.
        vector<int> dist(V, 1e9); 
        
        st.insert({0, S}); 

        // Source initialised with dist=0
        dist[S] = 0;
        
        // Now, erase the minimum distance node first from the set
        // and traverse for all its adjacent nodes.
        while(!st.empty()) {
            auto it = *(st.begin()); 
            int node = it.second; 
            int dis = it.first; 
            st.erase(it); 
            
            // Check for all adjacent nodes of the erased
            // element whether the prev dist is larger than current or not.
            for(auto it : adj[node]) {
                int adjNode = it[0]; 
                int edgW = it[1]; 
                
                if(dis + edgW < dist[adjNode]) {
                    // erase if it was visited previously at //this is where it gets faster
                    // a greater cost.
                    if(dist[adjNode] != 1e9) 
                        st.erase({dist[adjNode], adjNode}); 
                        
                    // If current distance is smaller,
                    // push it into the queue
                    dist[adjNode] = dis + edgW; 
                    st.insert({dist[adjNode], adjNode}); 
                 }
            }
        }
        // Return the list containing shortest distances
        // from source to all the nodes.
        return dist; 
    }
```

### Print the Shortest Path - 
given source and destination.
Now, to do this we will use memoization to know where are we coming from.
so we have our priority queue, distance array and another array, parent for remembering where we came from.
initially the parent array values will be the index values itself, and distances INT_MAX.
While updating the  distance, if we are updating the distance, we push it into the priority queue and then also mark the immediate parent of the node in the parent array by placing the parent value at the child index.
now, to figure out the path from this, we see the value at the destination in parent array, then we got to parent(parent(destination)) and so on, till we hit the source index. keep on printing at each step till then and done.
```C++
vector<int> shortestPath(int n, int m, vector<vector<int>> &edges)
    {
        // Create an adjacency list of pairs of the form node1 -> {node2, edge weight}
        // where the edge weight is the weight of the edge from node1 to node2.
        vector<pair<int, int>> adj[n + 1];
        for (auto it : edges)
        {
            adj[it[0]].push_back({it[1], it[2]});
            adj[it[1]].push_back({it[0], it[2]});
        }
        // Create a priority queue for storing the nodes along with distances 
        // in the form of a pair { dist, node }.
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int,int>>> pq;

        // Create a dist array for storing the updated distances and a parent array
        //for storing the nodes from where the current nodes represented by indices of
        // the parent array came from.
        vector<int> dist(n + 1, 1e9), parent(n + 1);  //both arrays 1-based
        for (int i = 1; i <= n; i++)
            parent[i] = i;

        dist[1] = 0; //distance of source 

        // Push the source node to the queue.
        pq.push({0, 1});
        while (!pq.empty())
        {
            // Topmost element of the priority queue is with minimum distance value.
            auto it = pq.top();
            pq.pop();
            int node = it.second;
            int dis = it.first;

            // Iterate through the adjacent nodes of the current popped node.
            for (auto it : adj[node])
            {
                int adjNode = it.first;
                int edW = it.second;

                // Check if the previously stored distance value is 
                // greater than the current computed value or not, 
                // if yes then update the distance value.
                if (dis + edW < dist[adjNode])
                {
                    dist[adjNode] = dis + edW;
                    pq.push({dis + edW, adjNode});

                    // Update the parent of the adjNode to the recent 
                    // node where it came from.
                    parent[adjNode] = node;
                }
            }
        }

        // If distance to a node could not be found, return an array containing -1.
        if (dist[n] == 1e9)
            return {-1};

        // Store the final path in the ‘path’ array.
        vector<int> path;
        int node = n;

        // Iterate backwards from destination to source through the parent array.
        while (parent[node] != node)
        {
            path.push_back(node);
            node = parent[node];
        }
        path.push_back(1);

        // Since the path stored is in a reverse order, we reverse the array
        // to get the final answer and then return the array.
        reverse(path.begin(), path.end());
        return path;
    }
```