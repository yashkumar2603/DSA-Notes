We are given a vector of vectors of size 3, the 2 nodes of the edge and the weight of the edge. find the shortest distance in O(n+e), dijkstra's works in O((n+e)logn).
So we make the adjacency list in the form of a vector of vector of vectors, we push the other node and the edge weight for each edge in every vector.
