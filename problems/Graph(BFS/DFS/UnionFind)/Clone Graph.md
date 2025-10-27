Leetcode 133

Problem:
Given a reference of a node in a connected undirected graph , return a deep copy(clone) of the graph.

Each node contains :
class Node{
    public int val;
    public List<Node> neighbors;
}

Example : 
Input :
adjList = [[2, 4], [1, 3], [2, 4], [1, 3]]

   1 —— 2
   |     |
   4 —— 3


Output : A cloned graph with same connections

Key Idea : 
To clone a graph, we must
1. Avoid infifnite loops in cycles
2. preserve connections between nodes

We use a HashMap<Node, Node> visited:
- Key -> Original node
- Value -> Cloned node

Then, we do DFS or BFS

For each node:

If not cloned → create clone and store in map.

For each neighbor → recursively clone and add to clone’s neighbor list.


                        class Solution {
                            private Map<Node, Node> visited = new HashMap<>();

                            public Node cloneGraph(Node node) {
                                if (node == null) return null;

                                // If already cloned, return from map
                                if (visited.containsKey(node)) {
                                    return visited.get(node);
                                }

                                // Clone the node (without neighbors)
                                Node clone = new Node(node.val, new ArrayList<>());
                                visited.put(node, clone);

                                // Clone all the neighbors
                                for (Node neighbor : node.neighbors) {
                                    clone.neighbors.add(cloneGraph(neighbor));
                                }

                                return clone;
                            }
                        }

Time complexity : O(V + E) -> each node and edge visisted once
Space complexity : O(v) -> HashMap + recursion stack or queue
