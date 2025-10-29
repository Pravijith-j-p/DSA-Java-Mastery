Leetcode 684

Problem : 
Given a graph with n nodes initially forming a tree (thus having n - 1 edges)
But then one extra edge is added  creating a cycle

Return the edge that,if removed , will make the graph a tree again
If multiple edges cause cycles, return the last one in the input

✅ Key Idea

Since a tree has no cycles, the first edge that tries to connect two already-connected nodes is the one that forms a cycle.

The problem reduces to:

Detect the first edge that connects two nodes already in the same connected component.

This is exactly what Union-Find (Disjoint Set Union) is good at.

✅ Approach — Union-Find
Logic

For each edge [u, v]:

Find roots of u and v.

If roots are same → adding this edge makes a cycle → return this edge.

Otherwise → union the nodes.

class Solution {
    public int[] findRedundantConnection(int[][] edges) {
        int n = edges.length;

        int[] parent = new int[n + 1];
        int[] rank = new int[n + 1];

        for (int i = 1; i <= n; i++) parent[i] = i;

        for (int[] e : edges) {
            int u = e[0], v = e[1];
            if (!union(u, v, parent, rank)) {
                return e; // this edge creates a cycle
            }
        }

        return new int[0];
    }

    private int find(int x, int[] parent) {
        if (parent[x] != x)
            parent[x] = find(parent[x]); // path compression
        return parent[x];
    }

    private boolean union(int x, int y, int[] parent, int[] rank) {
        int rootX = find(x, parent);
        int rootY = find(y, parent);

        if (rootX == rootY) return false; // cycle detected

        if (rank[rootX] < rank[rootY]) {
            parent[rootX] = rootY;
        } else if (rank[rootX] > rank[rootY]) {
            parent[rootY] = rootX;
        } else {
            parent[rootY] = rootX;
            rank[rootX]++;
        }

        return true;
    }
}

✅ Example
Input:
[[1,2],[1,3],[2,3]]


Processing:

Add (1,2) → OK

Add (1,3) → OK

Add (2,3) → both are already connected → ❗ cycle detected

Output:
[2,3]

Time complexity : O(n)
Space complexity : O(n)