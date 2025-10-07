Leetcode 226

Problem : Invert Binary Tree

Given the root of a binary tree, invert the tree, and return its root
Inversions means swapping the left and righ child of every node

Example : 

Input:
                            4
                          /   \
                         2     7
                        / \    /\
                       1   3  6  9

Output:
                            4
                          /   \
                         7     2
                        / \    /\
                       9   6  3  1


💡 Intuition

To invert a binary tree:
- At every node swap its left and right children
- Recursively repeat the same for left and right subtrees

You can use : 
1. Recursion (DFS) -> clean
2. Queue(BFS) -> Iterative approach

🔵 Brute Force (recursive)
Simpleset , most intutive - just swap and recurse

                                class Solution{
                                    public TreeNode invertTree(TreeNode root){
                                        if(root == null) return null;

                                        //Swap left and right
                                        TreeNode temp = root.left;
                                        root.left = root.right;
                                        root.right = temp;

                                        //Recurse
                                        invertTree(root.left);
                                        invertTree(root.right);

                                        return root;
                                    }
                                }

Time Complexity : O(n)
Space Complexity : O(h)-> height of tree

 ✅ Optimized approach (Iterative BFS)

                            class Solution{
                                public TreeNode invertTree(Treenode root){
                                    if(root ==null) return null;

                                    Queue<TreeNode> queue = new LinkedList<>();
                                    queue.add(root);

                                    while(!queue.isEmpty()){
                                        TreeNode node = queue.poll();

                                        //Swap
                                        TreeNode temp = node.left;
                                        node.left = node.right;
                                        node.right = temp;

                                        //Add children to the queue
                                        if(node.left!=null) queue.add(node.left);
                                        if(node.right!=null) queue.add(node.right);
                                    } 
                                    return root;
                                }
                            }
Time complexity : O(n)
Space Complexity  :O(n)

🔁 Pattern / Key Idea

Tree Traversal + Swap (DFS or BFS)
This problem teaches recursion fundamentals and symmetry patterns — useful for mirror tree, same tree, etc.
