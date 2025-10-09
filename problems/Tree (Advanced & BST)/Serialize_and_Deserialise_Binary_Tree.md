Leetcode 297

Problem : Given root of a Binary Tree .Design an alogorithm to serialise(convert it toa string) and deserialise(convert back to tree)
Serialise format can be anything, but it must allow accurate deserialisation

Example : 
Input : root=[1, 2, 3, null, null, 4, 5]
Output : "[1, 2, 3, null, null, 4, 5]"
Explanation :                                   1
                                                /\
                                               2  3
                                                  /\
                                                 4  5
After deserilisation you should get the same structure

Intution :
We can traverse the tree level-by-level(BFS) or preorder (DFS)

🔵 Brute Force Idea:
We can use preorder traversal and represent null nodes as "null"

Example tree:                               
                                                1
                                                /\
                                               2  3
                                                  /\
                                                 4  5
"1,2,null,null,3,4,null,null,5,null,null"

                                        class Solution{
                                            public String serialise(TreeNode root){
                                                if(root == null) return null;
                                                return root.val+" "+serialise(root.left)+ serialise(root.right);
                                            }
                                            //Decodes encoded data to tree
                                            public TreeNode desirialise(String data){
                                                String[] values = data.split(",");
                                                Queue<String> queue = new LinkedList<>(Arrays.asList(values));
                                                return buildTree(queue);
                                            }
                                            private TreeNode buildTree(Queue<String> queue){
                                                String val = queue.poll();
                                                if(val.equals("null")) return null;

                                                TreeNode node = new TreeNode(Integer.parseInt(val));
                                                node.left = buildTree(queue);
                                                node.right = buildTree(queue);
                                                return node;
                                            }   
                                        }
 Time Complexity: O(N)
 Space Complexity: O(N)
 Pattern: Level Order Traversal (BFS)

✅ Optimized approach(BFS -Level order)
Better for iterative deserialisation

                                        public class Codec{

                                            //Serialize using BFS
                                            public String serialize(TreeNode root){
                                                if(root == null) return "";
                                                StringBuilder sb = new StringBuilder();
                                                Queue<TreeNode> queue = new LinkedList<>();
                                                queue.offer(root);

                                                while(!queue.isEmpty()){
                                                    TreeNode node = queue.poll();
                                                    if(node == null){
                                                        sb.append("null,");
                                                        continue;
                                                    }
                                                    sb.append(node.val).append(",");
                                                    queue.offer(node.left);
                                                    queue.offer(node.right);
                                                }
                                                return sb.toString();
                                            }
                                            
                                            //Deserialise using BFS
                                            public TreeNode deserialize(String data){
                                                if(data.isEmpty()) return null;
                                                String [] values =data.split(",");
                                                TreeNode root = new TreeNode(Integer.parseInt(values[0]));
                                                Queue<TreeNode> queue = new LinkedList<>();
                                                queue.offer(root);

                                                int i = 1;
                                                while(!queue.isEmpty() && i < values.length) {
                                                    TreeNode node =queue.poll();

                                                    if(!values[i].equals("null")){
                                                        node.left = new TreeNode(Integer.parseInt(values[i]));
                                                        queue.offer(node.left);
                                                    }
                                                    i++;

                                                    if(i<values.length && !values[i].equals("null")){
                                                        node.right = new TreeNode(Integer.parseInt(values[i]));
                                                        queue.offer(node.right);
                                                    }
                                                    i++;
                                                }
                                                return root;
                                            }
                                        }

