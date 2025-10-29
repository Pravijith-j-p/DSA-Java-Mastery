Leetcode 261

Problem:
Given:
- n -> number of nodes labeled 0 to n-1
- edges[i] = [u, v] → undirected edge between u and v

Return true if the graph forms a valid tree, otherwise false.

🧠 Key Idea — What Makes a Graph a Tree?

A graph is a tree if and only if:

It is connected (all nodes reachable), AND

It has no cycles.

For an undirected graph with n nodes:

✅ A valid tree must have exactly n - 1 edges.

🔹 Example 1

Input:

n = 5
edges = [[0,1],[0,2],[0,3],[1,4]]


Output:
true

Explanation:
All nodes connected and no cycles.

🔹 Example 2

Input:

n = 5
edges = [[0,1],[1,2],[2,3],[1,3],[1,4]]


Output:
false

Explanation:
Contains a cycle (1–2–3–1).

⚙️ Approach 1 — DFS (Cycle Detection + Connectivity)
Steps

If edges.length != n - 1 → directly return false.

Build an adjacency list.

Use DFS to:

Track visited nodes.

Detect cycles.

After DFS, check if all nodes were visited → ensures connectivity.

                                class Solution {
                                    public boolean validTree(int n, int[][] edges) {
                                        if (edges.length != n - 1) return false; // Must have n-1 edges

                                        List<List<Integer>> graph = new ArrayList<>();
                                        for (int i = 0; i < n; i++)
                                            graph.add(new ArrayList<>());

                                        for (int[] e : edges) {
                                            graph.get(e[0]).add(e[1]);
                                            graph.get(e[1]).add(e[0]);
                                        }

                                        boolean[] visited = new boolean[n];
                                        if (hasCycle(graph, visited, 0, -1)) return false;

                                        // Ensure all nodes are connected
                                        for (boolean v : visited)
                                            if (!v) return false;

                                        return true;
                                    }

                                    private boolean hasCycle(List<List<Integer>> graph, boolean[] visited, int node, int parent) {
                                        visited[node] = true;
                                        for (int neighbor : graph.get(node)) {
                                            if (!visited[neighbor]) {
                                                if (hasCycle(graph, visited, neighbor, node))
                                                    return true;
                                            } else if (neighbor != parent) {
                                                return true; // Found a cycle
                                            }
                                        }
                                        return false;
                                    }
                                }
Time complexity : O(V + E)
Space complexity : O(V + E)

