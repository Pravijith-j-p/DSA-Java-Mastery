Leetcode 417

Problem : 
Given an m x n matrix of heights

Water can floe from a cell to another cell only if the next cell's height is <= current cell's height(i.e., downhill or equal)

There are two oceans:
- Pacific Ocean : touches the left and top edges
- Atlantic Ocean : touches the right and bottom edges

Return all coordinates where water can flow to both oceans

Example :
Input :
heights = [
  [1,2,2,3,5],
  [3,2,3,4,4],
  [2,4,5,3,1],
  [6,7,1,4,5],
  [5,1,1,2,4]
]

Output : 
[[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]


🧠 Intuition
Instead of starting from each cell and checking if it can reach the oceans (which would be expensive), we reverse the flow:

Start from the oceans and move inward.

From Pacific (top + left borders)

From Atlantic (bottom + right borders)

At each step, move uphill or flat (height ≥ current cell), since water could have flowed downhill in the forward direction.

Finally, the cells reachable from both Pacific and Atlantic are our result.

⚙️ Approach — DFS from Borders
Steps:
Create two boolean matrices:
pacific[m][n] and atlantic[m][n].

For each border cell of Pacific, run DFS.

For each border cell of Atlantic, run DFS.

Any cell that’s true in both → answer.

class Solution {
    private int[][] heights;
    private int m, n;
    private final int[][] directions = {{1,0},{-1,0},{0,1},{0,-1}};

    public List<List<Integer>> pacificAtlantic(int[][] heights) {
        this.heights = heights;
        m = heights.length;
        n = heights[0].length;

        boolean[][] pacific = new boolean[m][n];
        boolean[][] atlantic = new boolean[m][n];

        // Pacific (top + left edges)
        for (int i = 0; i < m; i++)
            dfs(i, 0, pacific, heights[i][0]);
        for (int j = 0; j < n; j++)
            dfs(0, j, pacific, heights[0][j]);

        // Atlantic (bottom + right edges)
        for (int i = 0; i < m; i++)
            dfs(i, n - 1, atlantic, heights[i][n - 1]);
        for (int j = 0; j < n; j++)
            dfs(m - 1, j, atlantic, heights[m - 1][j]);

        // Find cells reachable by both
        List<List<Integer>> result = new ArrayList<>();
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (pacific[i][j] && atlantic[i][j]) {
                    result.add(Arrays.asList(i, j));
                }
            }
        }
        return result;
    }

    private void dfs(int r, int c, boolean[][] visited, int prevHeight) {
        if (r < 0 || c < 0 || r >= m || c >= n) return;
        if (visited[r][c] || heights[r][c] < prevHeight) return;

        visited[r][c] = true;
        for (int[] d : directions) {
            dfs(r + d[0], c + d[1], visited, heights[r][c]);
        }
    }
}
