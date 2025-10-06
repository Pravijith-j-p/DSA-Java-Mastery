🌳 What is a Tree?

- A tree is an non-linear hierarchical data structure that consists of nodes connected by edges.

- it starts with a root node, and every node can have child nodes, except the leaf nodes(which have no children).

         1         ← Root
       /   \
      2     3
     / \   / \
    4  5  6   7   ← Leaves

🧩 Tree Terminology 

Term  |        definition                               |
------|------------------------------------------------ |
Node  | An element of tree containing data|             |
Root  | The topmost node of the tree                    |
Edge  | A link between a parent and a child node        |
Child | A node directly connected below another node    |
Parent| A node that has one or more children            |
Leaf  | A node with no children                         |
Height of a node| The number of edges on the longest path from the node to a leaf |
Depth of a node | The number of edges from the root to that node. |
Subtree | Any node and all its descendants              |

🧠 Properties of Trees
1. A tree with N nodes has exactly N -1 edges
2. There is exactly one path between any two nodes
3. The height of the tree = height of root node
4. Trees can be balanced or unbalanced

Type of Trees

1. General Tree 
- Each node can have any number of children
2. Binary Tree
- Each node can have atmost two children -left and right
3. Binary Search Tree
- A binary tree with additional property
    - Left child < Parent
    - Right child > Parent
    This property allows O(nlogn) search, insertion, and deletion (for balanced trees)
4. Balanced Trees
Example : AVL Tree, Red-Black Tree
They maintain balance to ensure logarithmic time operations

5. Complete binary tree
All levels are completely filled except possibly the last, which is filled from left to right.

6. Full Binary Tree
Every node has either 0 or 2 children

7. Perfect Binary tree
All internal nodes have two children and all leaves are at the same level

⚙️ Common Tree traversals
Tree traversals determine the order in which nodes are visited

1. Depth First Search (DFS)
a. Inorder(Left -> Root -> Right)
✅ Used in BST to get sorted order

b. Preorder(Root -> Left -> Right)
✅ Used for tree creation or expression trees

c. Postorder(Left -> Right -> Root)
✅ Used for deleting a tree

2. Breadth-First Search (BFS)/Level Order
✅ Traverse level by level using a queue

                            class Node{
                                int data;
                                Node left ,right;

                                Node(int data){
                                    this.data = data;
                                    left = right = null;
                                }
                            }

                            public class BinaryTree{
                                Node root;

                                void inorder(Node node){
                                    if (node == null) return;
                                    inorder(node.left);
                                    System.out.print(node.data + " ");
                                    inorder(node.right);
                                }

                                void preorder(Node node){
                                    if(node == null)return;
                                    System.out.print(node.data + " ");
                                    preorder(node.left);
                                    preorder(node.right);
                                }

                                void postorder(Node node){
                                    if(node == null) return;
                                    postorder(node.left);
                                    postorder(node.right);
                                    System.out.print(node.data + " ");
                                }

                                public static void main(String[]args){
                                    BinaryTree tree = new BinaryTree();
                                    tree.root = new Node(1);
                                    tree.root.left = new Node(2);
                                    tree.root.right = new Node(3);
                                    tree.root.left.left = new Node(4);

                                    System.out.print("Inorder: ");
                                    tree.inorder(tree.root);
                                }
                            }

🧩 Common Interview Questions (MAANG Level)
| Category          | Problem                                                |
| ----------------- | ------------------------------------------------------ |
| **Traversal**     | Inorder / Preorder / Postorder Traversal               |
| **View**          | Left View, Right View, Top View, Bottom View           |
| **Height**        | Find height or depth of the tree                       |
| **Path Problems** | Path sum, diameter, lowest common ancestor (LCA)       |
| **BST Specific**  | Validate BST, kth smallest element, insert/delete node |
| **Construction**  | Build tree from preorder & inorder traversal           |
| **Advanced**      | Serialize & Deserialize Binary Tree, Mirror Tree       |
