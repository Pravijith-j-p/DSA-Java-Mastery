Leetcode 323

Problem:
Given 
- n -> number of nodes (labeled 0 to n-1)
- edges[i] = [u, v] -> undirected edge between nodes u and v

Return the number of connected components in the graph

Example 1:
Input : 
n = 5
edges = [[0,1], [1,2], [3,4]]

Graph:
0 - 1 - 2       3 - 4

Output : 2
Two connected components : {0, 1, 2} and {3, 4}

🔹 Example 2

Input:

n = 5
edges = [[0,1],[1,2],[2,3],[3,4]]


Graph:

0 — 1 — 2 — 3 — 4


Output:
1
✅ All nodes are connected.

🧠 Concept

You can think of this as counting disjoint sets of connected nodes.

We can solve it using either:

DFS / BFS traversal, or

Union-Find (Disjoint Set Union)

⚙️ Approach 1 — DFS Traversal
Steps

Build an adjacency list.

Maintain a visited[] array.

For each unvisited node:

Start a DFS (or BFS)

Mark all reachable nodes as visited

Increment component count

                        class Solution {
                            public int countComponents(int n, int[][] edges) {
                                List<List<Integer>> graph = new ArrayList<>();
                                for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

                                // Build adjacency list
                                for (int[] e : edges) {
                                    graph.get(e[0]).add(e[1]);
                                    graph.get(e[1]).add(e[0]);
                                }

                                boolean[] visited = new boolean[n];
                                int components = 0;

                                for (int i = 0; i < n; i++) {
                                    if (!visited[i]) {
                                        dfs(graph, visited, i);
                                        components++;
                                    }
                                }

                                return components;
                            }

                            private void dfs(List<List<Integer>> graph, boolean[] visited, int node) {
                                if (visited[node]) return;
                                visited[node] = true;
                                for (int neighbor : graph.get(node)) {
                                    if (!visited[neighbor]) dfs(graph, visited, neighbor);
                                }
                            }
                        }
