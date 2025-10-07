Leetcode 199

Problem : 
Given the root of a binary tree, imagine yourself standing on the right side of it
Return the values of the nodes you can see ordered from top to bottom

Example : 
                                        1
                                        /\
                                       2  3
                                        \   \
                                        5    4
Output :
[1, 3, 4]

Intution : 
We need to collect the last node at each level when traversing the tree level by level
This can be done in two main ways:
1. BFS (Iterative) - Using a Queue
2. DFS (recursive) - visiting right nodes before left ones

Approach 1 :BFS (Level Order Trasversal)

                            class Solution {
                                public List<Integer> rightSideView(TreeNode root){
                                    List<inetegr> res = new ArrayList<>();
                                    if(root == null) return res;

                                    Queue<TreeNode> queue = new LinkedList<>();
                                    queue.offer(root);

                                    while(!queue.isEmpty()){
                                        int levelSize = queue.size();
                                        TreeNode rightMost = null;

                                        for(int i = 0;i<levelSize;i++){
                                            TreeNode node = queue.poll();

                                            if(i == levelSize - 1){
                                                res.add(node.val);
                                            }
                                            if(node.left != null)queue.offer(node.left);
                                            if(node.right != null)queue.offer(node.right);
                                        }
                                    }
                                    return res;
                                }
                            }
Time Complexity  : O(n) ->every node processed once
Space Complexity : O(n) 

Approach 2 :DFS (Right-First Traversal)

We do a preorder traversal(Root->Right->Left) and keep track of the depth
At each depth, if its the first node we encounter, its the rightmost one

                            class Solution{
                                public List<Integer> rightSideView(TreeNode root){
                                    List<Integer> res = new ArrayList<>();
                                    dfs(root, 0, res);
                                    return res;
                                }
                                private void dfs(TreeNode root, int depth, List<Integer> res){
                                    if(node == null) return;

                                    //First Node encountered at this depth
                                    if(depth == res.size()){
                                        res.add(node,val);
                                    }
                                    dfs(node.right, depth+1, res);
                                    dfs(node.left, depth+1, res);
                                }
                            }

🧩 Pattern / Key Idea

Pattern: Level Order Traversal (BFS) / Modified Preorder (DFS)

Data Structures: Queue (for BFS) or Recursion (for DFS)

Type: Tree Traversal / Right View Extraction