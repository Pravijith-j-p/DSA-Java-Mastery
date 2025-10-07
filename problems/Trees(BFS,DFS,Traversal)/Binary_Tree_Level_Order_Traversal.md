Leetcode 102

Problem : 
Given the root of a binary tree , return the level order traversal of its nodes' values
(From left to right,level by level)

Example : 
Input : 
                                        3
                                       / \
                                      9  20
                                         / \
                                        15  7
Output : 
[[3], [9, 20], [15, 7]]

Intutuon : 
We need to visit nodes level by level - this is a Breadth-First Search pattern
To achieve this , we use a queue(FIFO) structure that processes nodes in the order they appear in each level

Brute Force Approch(Recursive BFS simulation)

We can perform a recursive traversal while keeping track of the current level and appending nodes to lists corresponding to that level

Time Complexity : O(n)
Space Complexity : O(n)

                            class Solution{
                                public List<List<Integer>> levelOrder (TreeNode root){
                                    List<List<Integer>> res = new ArrayList<>();
                                    traverse(root, 0, res);
                                    return res;
                                }
                                private void traverse(TreeNode node, int level, List<List<Integer>> res){
                                    if(node == null) return;

                                    if(res.size() == level) {
                                        res.add(new ArrayList<>());
                                    }
                                    res.get(level).add(node.val);
                                    traverse(node.left, level+1, res);
                                    traverse(node.right, level+1, res);
                                }
                            }

✅ Optimized approach (Using Queue)

                            class Solution{
                                public List<List<Integer>> levelOrder(TreeNode root){
                                    List<List<Integer>> result = new ArrayList<>();
                                    if(root == null) return result;

                                    Queue<TreeNode> queue = new LinkedList<>();
                                    queue.offer(root);

                                    while(!queue.isEmpty()){
                                        int levelSize = queue.size();
                                        List<Integer> level = new ArrayList<>();

                                        for(int i = o;i< levelSize;i++){
                                            TreeNode node = queue.poll();
                                            level.add(node.val);

                                            if(node.left != null) queue.offer(node.left);
                                            if(node.right != null) queue.offer(node.right);
                                        }
                                            result.add(level);
                                    }
                                    return result;
                                }
                            }
    
🧩 Pattern / Key Idea

Pattern: Breadth-First Search (BFS)

Data Structure Used: Queue
