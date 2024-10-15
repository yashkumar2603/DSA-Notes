Here, we have to join them, but we cannot do BFS search for the  shortest path from island 1 to island 2.
As we will have to search starting from every node of island 1 and then try to reach island 2 somehow, - $O(n^4)$ 

To optimize this, we can use a combination of BFS and DFS 
We first find the first island using DFS and grab all the ones in it then start a multisource BFS from every 1 at once, basically expanding the island.

```C++
class Solution {
public:
    void dfs(vector<vector<int>>& A, vector<vector<bool>>& visited, queue<pair<int, int>>& q, int i, int j, vector<vector<int>>& dirs) {
        if(i<0 || j<0 || i>=A.size() || j>=A[0].size() || visited[i][j] || A[i][j] == 0)
            return ;
        
        visited[i][j]=true;
        q.push({i,j});
        for(auto& d:dirs)
            dfs(A, visited, q, i+d[0], j+d[1], dirs);
    }

    int shortestBridge(vector<vector<int>>& A) {
        int m=A.size(), n=A[0].size();
        vector<vector<bool>> visited(m, vector<bool>(n, false));
        vector<vector<int>> dirs = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
        queue<pair<int, int>> q;
        bool found=false;

        for(int i=0; i<m; i++)
        {
            for(int j=0; j<n; j++)
            {
                if(A[i][j]==1){
                    dfs(A, visited, q, i, j, dirs);
                    found=true;
                    break;
                }
            }
            if(found) break;
        }

        int steps=0;
        while(!q.empty())
        {
            int size=q.size();
            while(size-->0)
            {
                auto curr=q.front();
                q.pop();
                for(auto& d:dirs){
                    int i=curr.first + d[0];
                    int j=curr.second+d[1];

                    if(i>=0 && j>=0 && i<m && j<n && !visited[i][j]){
                        if(A[i][j]==1){
                            return steps; //found the other island;
                        }
                        q.push({i, j});
                        visited[i][j] = true;
                    }
                }
            }
            steps++;
        }
        return -1;
    }
};
```

