Leetcode 200

Given an m x n 2D grid map of '1's(land) and '0'(water), return the number of islands
An islands is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.

Example:
Input:

grid = [
  ['1','1','1','1','0'],
  ['1','1','0','1','0'],
  ['1','1','0','0','0'],
  ['0','0','0','0','0']
]

Output:
1

🏝️ What Counts as an Island?
An island is:

A group of '1's (land)

Connected horizontally or vertically (not diagonally)

Surrounded by '0's (water)

🔍 Step-by-Step Explanation
Let’s start scanning the grid from top-left:

Cell (0,0) is '1' → start DFS or BFS from here.

From (0,0), we can reach:

(0,1), (0,2), (0,3)

(1,0), (1,1), (1,3)

(2,0), (2,1)

All these '1's are connected directly or indirectly through horizontal/vertical paths.

Once we finish exploring this group, we mark all visited '1's as '0' (to avoid counting again).

Continue scanning the grid:

Every other cell is either '0' or already visited.

No new '1' is found that hasn’t already been counted.

✅ Final Result
Only one connected group of '1's was found.

Therefore, only one island exists.

🧠 Visualization Summary
Code
Island cells:
(0,0) → (0,1) → (0,2) → (0,3)
 ↓       ↓       ↓       ↓
(1,0) → (1,1)    X     (1,3)
 ↓       ↓
(2,0) → (2,1)
All these form one big island. No other '1's exist outside this group.

🔍 Step-by-Step DFS Traversal
Start scanning from top-left (0,0):

It’s '1' → this is unvisited land, so we start a DFS from here.

We mark this cell as visited (change to '0') and explore its neighbors.

DFS spreads to all connected '1's:

From (0,0) → right to (0,1), (0,2), (0,3)

Down to (1,0), (1,1), (1,3)

Further down to (2,0), (2,1)

All these are connected horizontally or vertically, so they belong to the same island.

Mark all visited land as '0':

After the DFS completes, all connected land cells are marked as '0'.

Continue scanning the grid:

Every other '1' has already been visited and marked as '0'.

No new unvisited '1' is found.

                                class Solution {
                                    public int numIslands(char[][] grid) {
                                        if (grid == null || grid.length == 0) return 0;

                                        int count = 0;
                                        int rows = grid.length;
                                        int cols = grid[0].length;

                                        // Traverse the grid
                                        for (int i = 0; i < rows; i++) {
                                            for (int j = 0; j < cols; j++) {
                                                // If land is found, start DFS
                                                if (grid[i][j] == '1') {
                                                    dfs(grid, i, j);
                                                    count++; // One island found
                                                }
                                            }
                                        }

                                        return count;
                                    }

                                    // DFS to mark all connected land as visited
                                    private void dfs(char[][] grid, int i, int j) {
                                        int rows = grid.length;
                                        int cols = grid[0].length;

                                        // Boundary and water check
                                        if (i < 0 || j < 0 || i >= rows || j >= cols || grid[i][j] == '0') return;

                                        grid[i][j] = '0'; // Mark as visited

                                        // Explore all 4 directions
                                        dfs(grid, i + 1, j); // down
                                        dfs(grid, i - 1, j); // up
                                        dfs(grid, i, j + 1); // right
                                        dfs(grid, i, j - 1); // left
                                    }
                                }
Time complexity : O(m * n)
Space complexity : O(m * n)

