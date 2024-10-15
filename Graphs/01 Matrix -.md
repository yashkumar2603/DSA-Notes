https://leetcode.com/problems/01-matrix/
```C++
class Solution {
public:
    //we need to find shortest route to the nearest 0,so bfs is better.
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        int m = mat.size();
        int n = mat[0].size();
        vector<vector<int>> ans(m, vector<int>(n, INT_MAX));
        queue<pair<int, int>> q;

        // Initialize the queue with all 0 cells and set their distance to 0
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (mat[i][j] == 0) {
                    ans[i][j] = 0;
                    q.push({i, j});
                }
            }
        }

        // Directions for the 4 possible movements
        vector<pair<int, int>> directions = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};

        // BFS from all 0 cells
        while (!q.empty()) {
            int i = q.front().first;
            int j = q.front().second;
            q.pop();

            for (auto dir : directions) {
                int ni = i + dir.first;
                int nj = j + dir.second;
                if (ni >= 0 && ni < m && nj >= 0 && nj < n) {
                    if (ans[ni][nj] > ans[i][j] + 1) { 
                        ans[ni][nj] = ans[i][j] + 1;
                        q.push({ni, nj});
                    }
                }
            }
        }

        return ans;
    }
};
```

