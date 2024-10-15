We apply the normal topo sort using BFS, but what happens is that out of the cyclic elements none will have indegree 0, so the queue will remain empty as nothing will be pushed in it, so the loop exits. 
So, if the return vector does not have the same length as the input number of vertices, there is a cycle in the graph.
