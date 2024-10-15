or to which connected component does a specific node belong to
graph is connected or disconnected?(components 1 or >1) 

To find the connected component, maintain a visited array and then when u visit any node, mark it in the array.
Whenever u find an unvisited element in the array, traverse as much as possible from it using either BFS or DFS and keep marking visited.
now just repeat
O(n)
