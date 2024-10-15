```C++
// 1.DFS(Recursion)
class Solution {
    bool isvalid(int i,int j,int n,int m){
        if(i>=0 && i<n && j>=0 && j<m){
            return 1;
        }
        return 0;
    }
    //nr, nc ->new
    // pi, pj->current(parent)
    bool find(int r,int c,vector<vector<char>>& grid,vector<vector<int>>&vis,int pi,int pj){
        vis[r][c]=1;
        int row[4]={0,0,-1,1};
        int col[4]={-1,1,0,0};
            for(int i=0;i<4;i++){
                int nr=r+row[i];
                int nc=c+col[i];
                if(isvalid(nr,nc,grid.size(),grid[0].size()) && grid[nr][nc]==grid[r][c]){
                    if(vis[nr][nc]==0){
                        if(find(nr,nc,grid,vis,r,c)){
                            return 1;
                        };
                    }
                    else if(pi!=nr || pj!=nc){
                        return 1;
                    }
                    
                }
            }
        
            return 0;
    }
public:
    bool containsCycle(vector<vector<char>>& grid) {
        int n=grid.size();
        int m=grid[0].size();
        vector<vector<int>>vis(n,vector<int>(m,0));

        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(vis[i][j]==0){
                    if(find(i,j,grid,vis,-1,-1)){
                        return 1;
                    }
                }
            }
        }
        return 0;
    }
};
```


