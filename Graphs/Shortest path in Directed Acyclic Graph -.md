# Relaxation of Edges - 
1. Topo-sort on the graph
2. Take a distance array and relax the edges, make distance of source = 0
3. take the source node, then go to its children - update their distance to be min(dist(child), dist(source)+weight(child)); (dist(source) is the distance from the source if the same node appears in another path)
4. keep on doing this for all elements in the array.
5. and now the distance array has the shortest distance of the node from the source or each node.

```C++
vector<int> toposort(int V, vector<vector<pair<int, int>>> &gr) {
    // Calculate in-degree of every node
    vector<int> indegree(V, 0);
    for (int node = 0; node < V; node++) {
        for (auto ne : gr[node]) {
            indegree[ne.first]++;
        }
    }
    // Push elements with in-degree 0 into the queue
    queue<int> q;
    for (int node = 0; node < V; node++) {
        if (indegree[node] == 0)
            q.push(node);
    }
    // Topological Sort
    vector<int> tSort;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        tSort.push_back(node);
        for (auto ne : gr[node]) {
            indegree[ne.first]--;
            if (indegree[ne.first] == 0)
                q.push(ne.first);
        }
    }

    // Shortest path initialization
    vector<int> dist(V, INT_MAX);
    dist[0] = 0; // Assuming 0 as the source
    // Distance relaxation
    for (int i = 0; i < V; i++) {
        int node = tSort[i];
        for (auto ne : gr[node]) {
            int neighbor = ne.first;
            int weight = ne.second;
            if (dist[node] + weight < dist[neighbor]) {
                dist[neighbor] = dist[node] + weight;
            }
        }
    }
    return dist;
}
```



