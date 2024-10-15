<font color="#f79646">Very Common Problem, read nicely.</font>

Go to every place u find one, go as far as possible in connected one cells, mark all cells visited with 0 and then repeat if u find any other 1.

```C++
class Solution {
public:
    void dfs(int row, int col, vector<vector<char>>& grid, int rows, int cols) {
        if (row < 0 || col < 0 || row >= rows || col >= cols ||
            grid[row][col] != '1')
            return;
        grid[row][col] = '0';
        dfs(row - 1, col, grid, rows, cols);
        dfs(row + 1, col, grid, rows, cols);
        dfs(row, col - 1, grid, rows, cols);
        dfs(row, col + 1, grid, rows, cols);
    };
    int numIslands(vector<vector<char>>& grid) {
        if (grid.empty() || grid[0].empty())
            return 0;

        int rows = grid.size();
        int cols = grid[0].size();
        int islands = 0;

        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                if (grid[row][col] == '1') {
                    dfs(row, col, grid, rows, cols);
                    islands++;
                }
            }
        }

        return islands;
    }
};
```
