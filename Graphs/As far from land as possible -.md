In this problem, we can either search from each 0 cell the nearest 1 cell O(n^4) time complexity 
ot we can run multiple bfs at parallel, that is from all the 1 cell, do simple bfs to reach 0.
So, take all 1 cells and push into queue beforehand and then do normal bfs.
```C++
class Solution {
public:
    int maxDistance(vector<vector<int>>& grid) {
        int n = grid.size();
        queue<pair<int, int>> q;
        vector<vector<int>> visited = grid;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (visited[i][j] == 1)
                    q.push({i, j});
            }
        }

        if (q.empty() || q.size() == n * n)
            return -1;

        int distance = 0;
        vector<pair<int, int>> dirs = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        while (!q.empty()) {
            int size = q.size();
            while (size--) {
                auto [x, y] = q.front();
                q.pop();
                for (auto [dx, dy] : dirs) {
                    int i = x + dx, j = y + dy;
                    if (i >= 0 && i < n && j >= 0 && j < n &&
                        visited[i][j] == 0) {
                        visited[i][j] = 1;
                        q.push({i, j});
                    }
                }
            }
            distance++;
        }
        return distance - 1;
    }
};
```

