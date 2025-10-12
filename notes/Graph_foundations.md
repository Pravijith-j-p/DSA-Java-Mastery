Graph is a collection of :
 - Vertices(Nodes) -> represent entities
 - Edges (Links) -> represent connections between them

 Example :

                                        A --- B
                                        |   / |
                                        |  /  |
                                        C ----D

Here : 
Vertices = {A, B, C, D}
Edges = {(A, B), (A, C), (B, C), (B, D), (C, D)}

🔵 1 . Adjacency Matrix
Definition :
An adjacency matrix is a 2D array (or matrix) where each cell (i, j) represents whether there is an edge from vertex i to vertex j

Example :
Let number vertices as 
A -> 0
B -> 1
C -> 2
D -> 3

Then the graph

                                        A --- B
                                        |   / |
                                        |  /  |
                                        | /   |
                                        C --- D

|   | A | B | C | D |
| - | - | - | - | - |
| A | 0 | 1 | 1 | 0 |
| B | 1 | 0 | 1 | 1 |
| C | 1 | 1 | 0 | 1 |
| D | 0 | 1 | 1 | 0 |

1 -> edge exits
0 -> no edge

int vertices = 4;
int [][] adjMatrix = new int [vertices][vertices];

//Add edge A-B
adjMatrix[0][1] = 1;
adjMatrix[1][0] = 1;

//Add edge A-C
adjMatrix[0][2] = 1;
adjMatrix[2][0] = 1;

//Add edge B-C
adjMatrix[1][2] = 1;
adjMatrix[2][1] = 1;

//Add edge B-D
adjMatrix[1][3] = 1;
adjMatrix[3][1] = 1;

//Add edge C-D
adjMatrix[2][3] = 1;
adjMatrix[3][2] = 1;

🔵 Adjacency List

Definition :
Each vertex stores a list of its adjacent vertices
Think of it as a HashMap or ArrayList where each vertex points to its neighbors.

Example :
                                                A --- B
                                                |   / |
                                                |  /  |
                                                C ----D

A → [B, C]
B → [A, C, D]
C → [A, B, D]
D → [B, C]

                            import java.util.*;

                            class Graph {
                                private int vertices;
                                private LinkedList<Integer>[] adjList;

                                Graph(int v) {
                                    vertices = v;
                                    adjList = new LinkedList[v];
                                    for (int i = 0; i < v; i++)
                                        adjList[i] = new LinkedList<>();
                                }

                                void addEdge(int src, int dest) {
                                    adjList[src].add(dest);
                                    adjList[dest].add(src); // remove this line for a directed graph
                                }

                                void printGraph() {
                                    for (int i = 0; i < vertices; i++) {
                                        System.out.print(i + " → ");
                                        for (int neighbor : adjList[i])
                                            System.out.print(neighbor + " ");
                                        System.out.println();
                                    }
                                }
                            }

                            public class Main {
                                public static void main(String[] args) {
                                    Graph g = new Graph(4);
                                    g.addEdge(0, 1);
                                    g.addEdge(0, 2);
                                    g.addEdge(1, 2);
                                    g.addEdge(1, 3);
                                    g.addEdge(2, 3);

                                    g.printGraph();
                                }
                            }
0 → 1 2 
1 → 0 2 3 
2 → 0 1 3 
3 → 1 2 


