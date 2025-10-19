Leetcode 79

Problem :
Given an m x n grid of characters board and a string word,
return true if the word exists in the grid

The word can be constructed from letters of sequentially adjacent cells,
where adjacent cells are horizontally or vertically neighbouring

The same letter cell cannot be used more than once

Example : 
Input : 

board = [
    ['A', 'B', 'C', 'E'],
    ['S', 'F', 'C', 'S'],
    ['A', 'D', 'E', 'E']
]
word = "ABCCED"

Output : true

Explanation : 
A -> B -> C -> C -> E -> D forms the word "ABCCED"  by valid moves

⚙️ Approach - Backtracking + DFS

1. Iterate over every cell in the grid
2. When the current cell's character matches the first letter of word, start a DFS
3. At each recursive step:
    - Check boundary and visited conditions
    - Compare current character with the word's current index
    - Mark the cell as visited (temporarly)
    - Explore 4 directions (up, down, left, right)
    - Restore the cell(backtrack)
4. Return true if any path matches the full word

class Solution{
        public boolean exist(char[][] board, String word){
            int m = board.length;
            int n = board[0].length;

            for(int i=0;i < m;i++){
                for(int j = 0;j<n;j++){

                    if(dfs(board, word, i, j, 0)){
                        return true;
                    }
                }
            }
            return false;
        }
        private boolean dfs(char[][] board, String word, int i, int j, int index){
            //base case : found word
            if(index == word.length()) return true;

            //boundary and character check
            if(i<0 || i>= board.length || j<0 || j >= board[0].length || board[i][j] != word.charAt(index)){
                return false;
            }

            //mark as visited
            char temp = board[i][j];
            board[i][j] = '#';

            //explore all 4 directions
            boolean found = dfs(board, word, i + 1, j, index + 1)
                          ||dfs(board, word, i - 1, j, index + 1) 
                          ||dfs(board, word, i, j + 1, index + 1)
                          ||dfs(board, word, i, j - 1, index + 1);

            //backtrack (restore)
            board[i][j] = temp;

            return found;
        }

}