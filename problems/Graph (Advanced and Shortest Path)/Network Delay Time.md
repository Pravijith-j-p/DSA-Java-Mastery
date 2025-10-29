Leetcode 743

Problem Summary

You are given:

times: list of directed edges (u, v, w)
meaning signal travels from u → v in w time.

n: number of nodes

k: starting node

Goal:

Return the time it takes for all nodes to receive the signal starting from k.
If some node cannot be reached → return -1.

✅ Why Dijkstra?

All edge weights are positive → ✅ Dijkstra is optimal.

We need single-source shortest path.

Result = max shortest distance among all nodes.

✅ Approach Summary

Build adjacency list.

Run Dijkstra from starting node k.

Track shortest times to each node.

Answer = max time.
If any node unreachable → return -1.

                            class Solution {
                                public int networkDelayTime(int[][] times, int n, int k) {
                                    List<List<int[]>> graph = new ArrayList<>();
                                    for (int i = 0; i <= n; i++) graph.add(new ArrayList<>());

                                    // Build graph: u -> (v, weight)
                                    for (int[] t : times) {
                                        graph.get(t[0]).add(new int[]{t[1], t[2]});
                                    }

                                    // Min-heap: (dist, node)
                                    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] - b[0]);
                                    pq.offer(new int[]{0, k});

                                    int[] dist = new int[n + 1];
                                    Arrays.fill(dist, Integer.MAX_VALUE);
                                    dist[k] = 0;

                                    while (!pq.isEmpty()) {
                                        int[] curr = pq.poll();
                                        int d = curr[0], node = curr[1];

                                        if (d > dist[node]) continue;

                                        for (int[] next : graph.get(node)) {
                                            int nei = next[0], w = next[1];

                                            if (dist[node] + w < dist[nei]) {
                                                dist[nei] = dist[node] + w;
                                                pq.offer(new int[]{dist[nei], nei});
                                            }
                                        }
                                    }

                                    int max = 0;
                                    for (int i = 1; i <= n; i++) {
                                        if (dist[i] == Integer.MAX_VALUE) return -1;
                                        max = Math.max(max, dist[i]);
                                    }

                                    return max;
                                }
                            }

Time complexity : O(E log V)
Space complexity : O(v  + E)
