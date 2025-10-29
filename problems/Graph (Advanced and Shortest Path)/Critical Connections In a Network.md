Leetcode 1192

✅ Problem Summary

You are given:

n nodes labeled 0 … n-1

A list of connections where each edge is bidirectional

Your task:
✅ Find all critical edges (bridges)
Removing any such edge increases the number of connected components.

✅ Pattern / Key Idea
✔️ Tarjan’s Algorithm (DFS + Low-Link Values)

For each node:

disc[u] = discovery time (DFS order)

low[u] = earliest discovered node reachable from u
(via DFS tree + back-edges)

An edge (u, v) is a bridge if:

low[v] > disc[u]


Meaning:
v cannot reach u or any ancestor of u without using edge (u → v).

✅ Step-by-Step Logic

Build adjacency list for the graph.

Run DFS from node 0.

Track:

discovery time array

low-link array

parent

For each edge (u → v):

If v is not visited → DFS to v
and update low[u] = min(low[u], low[v])

If back-edge → update low[u]

Check if it's a bridge:

if (low[v] > disc[u]) → critical edge

                                class Solution {

                                    private int time = 0;
                                    private List<List<Integer>> graph = new ArrayList<>();
                                    private List<List<Integer>> result = new ArrayList<>();
                                    private int[] disc, low;

                                    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {

                                        disc = new int[n];
                                        low = new int[n];
                                        Arrays.fill(disc, -1);

                                        // Build graph
                                        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());
                                        for (List<Integer> edge : connections) {
                                            int u = edge.get(0);
                                            int v = edge.get(1);
                                            graph.get(u).add(v);
                                            graph.get(v).add(u);
                                        }

                                        // DFS from node 0 (graph may be connected per problem)
                                        dfs(0, -1);

                                        return result;
                                    }

                                    private void dfs(int u, int parent) {
                                        disc[u] = low[u] = time++;

                                        for (int v : graph.get(u)) {
                                            if (v == parent) continue;

                                            if (disc[v] == -1) {
                                                dfs(v, u);
                                                low[u] = Math.min(low[u], low[v]);

                                                if (low[v] > disc[u]) {
                                                    result.add(Arrays.asList(u, v));  // critical edge
                                                }
                                            } else {
                                                low[u] = Math.min(low[u], disc[v]);  // back-edge
                                            }
                                        }
                                    }
                                }
Time complexity : O( V + E)
Space complxity : O(V + E)
