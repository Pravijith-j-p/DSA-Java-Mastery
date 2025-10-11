Leetcode 212

Problem : 
Given an m x n board of characters and a list of Strings words
Return all words on the board that can be formed by tracking letters adjacent (horizontally or vertically).

You may not reuse the same cell in a single word

Example:
Input:
board = [
    ['o', 'a', 'a', 'n'],
    ['e', 't', 'a', 'e'],
    ['i', 'h', 'k', 'r'],
    ['i', 'f', 'l', 'v']
]
words = ["oath", "pea", "eat", "rain"]

Output:
["oath", "eat"]

Intution : 
Brut forcing each word on the grid (O(W * M * N * 4^L)) is too slow
Insted we : 
1. Build a trie of each words
2. DFS from every cell on the board
3. Bactrack while marking visited cells
4. Use the trie to prune invalid paths early (no prefix match ->stop)

🔵 Brute force approach (Without Trie)

Idea :
-  for each word, check if it exists in the board using DFS

Complexity : O(W * M * N * 4^L) -> W = number of words, L = length of longest word.

Space : O(L) -> recursion stack

                                                class Solution {
                                                    public List<String> findWords(char[][] board, String [] words){
                                                        List<String> result = new ArrayList<>();
                                                        for(String word : words){
                                                            if(exist(board, word)) result.add(word);
                                                        }
                                                        return result;
                                                    }

                                                    private boolean exist(char[][] board,  String word){
                                                        int m = board.length, n = board[0].length;
                                                        boolean[][] visited = new boolean [m][n];

                                                        for(int i = 0;i<m;i++){
                                                            for(int j =0;j<n;j++){
                                                                if(dfs(board, word, 0, i, j, visisted)) return true;
                                                            }
                                                        }
                                                        retur false;
                                                    }

                                                    private boolean dfs(char[][] board, String word, int idx, int i, boolean[][] visited){
                                                        if(idx == word.length()) return true;
                                                        if (i < 0 || j < 0 || i >= board.length || j >= board[0].length ||
                                                            visited[i][j] || board[i][j] != word.charAt(idx)) return false;

                                                        visited[i][j] = true;
                                                        boolean found = dfs(board, word, idx + 1, i + 1, j, visited)
                                                                    || dfs(board, word, idx + 1, i - 1, j, visited)
                                                                    || dfs(board, word, idx + 1, i, j + 1, visited)
                                                                    || dfs(board, word, idx + 1, i, j - 1, visited);
                                                        visited[i][j] = false;
                                                        return found;
                                                    }
                                                }

✅ Optimized Approach (Trie + DFS + Backtracking)

Idea :
1. Insert all words into a Trie
2. From each cell, DFS while checking valid prefixes in the Trie
3. Mark visisted cells and restore them after recursion
4. When a Trie node's word field is not null -> found a word!

Complexity : 
Time : Time: O(M * N * 4^L) worst case
Space: O(sum of word lengths) for Trie + recursion.


                                            class TrieNode {
                                                TrieNode[] children = new TrieNode[26];
                                                String word = null;
                                            }

                                            class Solution {
                                                private TrieNode buildTrie(String[] words) {
                                                    TrieNode root = new TrieNode();
                                                    for (String word : words) {
                                                        TrieNode node = root;
                                                        for (char c : word.toCharArray()) {
                                                            int idx = c - 'a';
                                                            if (node.children[idx] == null)
                                                                node.children[idx] = new TrieNode();
                                                            node = node.children[idx];
                                                        }
                                                        node.word = word;
                                                    }
                                                    return root;
                                                }

                                                public List<String> findWords(char[][] board, String[] words) {
                                                    List<String> result = new ArrayList<>();
                                                    TrieNode root = buildTrie(words);

                                                    for (int i = 0; i < board.length; i++) {
                                                        for (int j = 0; j < board[0].length; j++) {
                                                            dfs(board, i, j, root, result);
                                                        }
                                                    }
                                                    return result;
                                                }

                                                private void dfs(char[][] board, int i, int j, TrieNode node, List<String> result) {
                                                    char c = board[i][j];
                                                    if (c == '#' || node.children[c - 'a'] == null) return;
                                                    node = node.children[c - 'a'];
                                                    if (node.word != null) {
                                                        result.add(node.word);
                                                        node.word = null; // avoid duplicates
                                                    }

                                                    board[i][j] = '#'; // mark visited
                                                    if (i > 0) dfs(board, i - 1, j, node, result);
                                                    if (j > 0) dfs(board, i, j - 1, node, result);
                                                    if (i < board.length - 1) dfs(board, i + 1, j, node, result);
                                                    if (j < board[0].length - 1) dfs(board, i, j + 1, node, result);
                                                    board[i][j] = c; // restore
                                                }
                                            }
