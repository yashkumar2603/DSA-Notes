[Shortest Path in a Grid with Obstacles Elimination - LeetCode](https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/description/)

This is different from normal as we will be visiting the same cell twice if the k value of the unit in bfs is different between the two so that makes a new thing

```C++
class Solution {
public:
    int shortestPath(vector<vector<int>>& grid, int k) {
        int m=grid.size(), n=grid[0].size();
        vector<vector<vector<bool>>> v(m, vector<vector<bool>>(n, vector<bool>(k+1)));
        //maintain state of visited of each cell
        queue<vector<int>> q; //used to maintain current position and neighbours position, we can also use pair if needed instead of vector
		q.push({0,0,k});
        int steps=0;
        vector<pair<int, int>> dirs = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};

        while(!q.empty())
        {
            int size=q.size();
            while(size-- >0){
                vector<int> curr=q.front();
                q.pop();
                if(curr[0]==m-1 && curr[1]==n-1) return steps;  //reached bottom right
                
                for(vector<int>& d:dirs){
                    int i=curr[0]+d[0];
                    int j=curr[1]+d[1];
                    int obs=curr[2];

                    if(i>=0 && i<m && j>=0 && j<n){
                        if(grid[i][j]==0 && !v[i][j][obs])
                            q.push({i, j, obs});
                            v[i][j][obs]=true;

                        else if(grid[i][j]==1 && obs>0 && !v[i][j][obs-1])
                        {
                            q.push({i,j,obs-1});
                            v[i][j][obs-1]=true;
                        }
                    }
                }
            }
            ++steps;
        }
        return -1;
    }
};
```

