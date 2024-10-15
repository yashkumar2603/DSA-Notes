In this, we have to reach the right bottom cell from the top left cell.
To do this, we spread to all directions then try to reach in as few steps as possible.
Since we "spread" we use aw breadth first search algo 
[Shortest Path in Binary Matrix - LeetCode](https://leetcode.com/problems/shortest-path-in-binary-matrix/description/)

In this problem, we use BFS and not DP because all  8 directions are allowed for us, but in dp only 4 directions are suitable, in dp solution, we only check down and left and right, but here we can also go up and in the diagonals as well
so no dp 

```C++
class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        if (grid[0][0] == 1 || grid[m - 1][n - 1] == 1)
            return -1;

        int dir[][2] = {{0, 1},  {0, -1}, {1, 0},   {-1, 0},
                        {1, -1}, {-1, 1}, {-1, -1}, {1, 1}};
        vector<vector<bool>> visited(m, vector<bool>(n, false));
        visited[0][0] = true;
        queue<vector<int>> q;  //maintains our position, an also take as a pair rather than vector.
        q.push({0, 0});

        int ans = 0;
        while (!q.empty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                auto curr = q.front();
                q.pop();
                if (curr[0] == m - 1 && curr[1] == n - 1) {
                    return ans + 1;
                }
                for (int k = 0; k < 8; k++) {
                    int nextX = dir[k][0] + curr[0];
                    int nextY = dir[k][1] + curr[1];

                    if (nextX >= 0 && nextX < m && nextY >= 0 && nextY < n &&
                        !visited[nextX][nextY] && grid[nextX][nextY] == 0) {
                        q.push({nextX, nextY});
                        visited[nextX][nextY] = true;
                    }
                }
            }
            ans++;
        }
        return -1;
    }
};
```

We take the size of the queue and then iterate on it as we will be adding new neighbours after that size in the queue.
Modifications to make code efficient edits the original array 
tell interviewer its not recommended to do this in production code but risky
