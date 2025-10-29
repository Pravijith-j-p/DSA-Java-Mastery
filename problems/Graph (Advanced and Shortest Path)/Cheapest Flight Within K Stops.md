Problem Summary

You are given:

flights: edges of the form (u, v, w) meaning cost w to fly from u → v

n: total number of cities

src: starting city

dst: destination city

k: maximum allowed stops (intermediate nodes)

Goal:
Find the minimum cost to travel from src → dst with at most k stops.
If no such route exists, return -1.

✅ Pattern / Key Idea
Bellman–Ford with (k + 1) relaxations

We perform k + 1 iterations, because:

k stops = k + 1 edges

Each iteration represents taking one more edge (one more “layer” of the route).

❇️ Bellman–Ford is ideal here because it:

explores all paths within the stop limit

updates costs even if a cheaper route appears later

does not incorrectly prune valid paths (unlike Dijkstra for this problem)

Thus it guarantees the correct minimum cost under the constraint of at most k stops.

                        class Solution {
                            public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {

                                int[] dist = new int[n];
                                Arrays.fill(dist, Integer.MAX_VALUE);
                                dist[src] = 0;

                                // We can make at most k stops → k+1 edges
                                for (int i = 0; i <= k; i++) {
                                    int[] temp = dist.clone();

                                    for (int[] f : flights) {
                                        int u = f[0], v = f[1], w = f[2];

                                        if (dist[u] != Integer.MAX_VALUE && dist[u] + w < temp[v]) {
                                            temp[v] = dist[u] + w;
                                        }
                                    }

                                    dist = temp;
                                }

                                return dist[dst] == Integer.MAX_VALUE ? -1 : dist[dst];
                            }
                        }

Time complexity : O(k * E)
Space complexity : O(v)

