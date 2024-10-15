The problem of rotting oranges can be visualized as a multi-source breadth-first search (BFS) where each rotten orange spreads its rot to adjacent fresh oranges over time. Each rotten orange at time `t` will rot its adjacent fresh oranges at time `t+1`. We need to keep track of the time taken to rot all oranges and check if there are any fresh oranges left unrotted.

# Approach

1. Initialize a queue and push all the initial positions of rotten oranges with time `0`.
2. Use BFS to process each cell. For each rotten orange, rot its adjacent fresh oranges and add them to the queue with the incremented time.
3. Keep track of the maximum time taken during the BFS traversal.
4. After the BFS traversal, check if there are any fresh oranges left. If yes, return `-1`, otherwise return the maximum time taken.

# Complexity

- **Time complexity:** (O(n×m))(O(n \times m))(O(n×m)), where (n) is the number of rows and (m) is the number of columns. Each cell is processed once.
- **Space complexity:** (O(n×m)),(O(n \times m)),(O(n×m)), used for the queue and the visited matrix.

```C++
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        int n =grid.size();
        int m = grid[0].size();

        vector<vector<int>>vis(n,vector<int>(m,0));
        queue<pair<pair<int,int>,int>>q;
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(grid[i][j]==2){ q.push({{i,j},0}); vis[i][j]=1;}
            }
        }
        int times=0;
        vector<int>xs={1,0,-1,0};
        vector<int>ys={0,1,0,-1};
        while(!q.empty()){
          int x=q.front().first.first;
          int y=q.front().first.second;
          int time=q.front().second;
          times=max(time,times);
          q.pop();
          for(int i=0;i<4;i++){
            int x1=x+xs[i];
            int y1=y+ys[i];
            if(x1>=0&&x1<n&&y1>=0&&y1<m&&vis[x1][y1]==0&&grid[x1][y1]==1){
                q.push({{x1,y1},time+1});
                vis[x1][y1]=1;
                grid[x1][y1]=2;
            }
          }

         
        }
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(grid[i][j]==1) return -1;
            }
        }
        return times;
    }
};
```

