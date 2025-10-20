Leetcode 51

Problem statement

Given an integer n
Place n queens on an n x n chessboard such that no two queens attack each other
Return all possible distinct solutions

Each solution is represented as a list of strings , where 'Q' and '.' denote a queen an an empty space respectively

Example :
Input : 
 n = 4

Output:
[
    [".Q.."],
    ["...Q"],
    ["Q..."],
    ["..Q."],

    ["..Q."],
    ["Q..."],
    ["...Q"],
    [".Q.."]
]

♟️ Constraints

Queens can attack along the same row, same column, and both diagonals.

We need to ensure none of these conflicts happen.


🧠 Key Idea — Backtracking

We place queens row by row, ensuring:

No other queen is in the same column.

No other queen is on the same diagonal.

We use recursion to explore each row, and if we reach beyond the last row, we have found a valid configuration.

⚙️ Approach

- Use a recursive function backtrack(row) to try placing a queen in each column of the current row.

- Maintain three sets to track attacks:

    - cols → columns where queens exist.

    - diag1 → “r - c” (↘ diagonal)

    - diag2 → “r + c” (↙ diagonal)

- If a column or diagonal is attacked, skip that position.

- If we reach row == n, we found a valid arrangement.

import java.util.*;

                    class Solution {
                        public List<List<String>> solveNQueens(int n) {
                            List<List<String>> result = new ArrayList<>();
                            char[][] board = new char[n][n];
                            for (char[] row : board) Arrays.fill(row, '.');

                            backtrack(0, board, result, new HashSet<>(), new HashSet<>(), new HashSet<>(), n);
                            return result;
                        }

                        private void backtrack(int row, char[][] board, List<List<String>> result,
                                            Set<Integer> cols, Set<Integer> diag1, Set<Integer> diag2, int n) {
                            if (row == n) {
                                result.add(construct(board));
                                return;
                            }

                            for (int col = 0; col < n; col++) {
                                if (cols.contains(col) || diag1.contains(row - col) || diag2.contains(row + col))
                                    continue;

                                // Choose
                                board[row][col] = 'Q';
                                cols.add(col);
                                diag1.add(row - col);
                                diag2.add(row + col);

                                // Explore
                                backtrack(row + 1, board, result, cols, diag1, diag2, n);

                                // Un-choose (backtrack)
                                board[row][col] = '.';
                                cols.remove(col);
                                diag1.remove(row - col);
                                diag2.remove(row + col);
                            }
                        }

                        private List<String> construct(char[][] board) {
                            List<String> res = new ArrayList<>();
                            for (char[] row : board) res.add(new String(row));
                            return res;
                        }

                        public static void main(String[] args) {
                            Solution s = new Solution();
                            List<List<String>> solutions = s.solveNQueens(4);
                            for (List<String> sol : solutions) {
                                for (String row : sol) System.out.println(row);
                                System.out.println();
                            }
                        }
                    }


🧮 Complexity Analysis
Type	Complexity
Time Complexity	O(N!) — because each row has up to N possible positions, and we prune invalid ones
Space Complexity	O(N²) for the board + recursion stack and tracking sets


