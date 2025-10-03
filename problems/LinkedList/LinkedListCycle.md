Leetcode 141

Problem : Given the head of a linkedlist, determine if the linkedlist has a cycle
A cycle exists if a node's next pointer points back to a previous node

Exmaple : Input head = [3 -> 2 -> 0 -> -4]

Output : true

Input : head = [1 -> 2 -> null]
Output : false


🟢 Brute Force Approach (HashSet)

Idea :
If we see the same node again -> cycle exists
If we reach null -> no cycle

                        public boolean hasCycle(ListNode head){
                            HashSet<ListNode> visited = new HashSet<>();
                            ListNode curr = head;

                            while (curr != null){
                                if(visisted.contains(curr)) return true;
                                visisted.add(curr);
                                curr = curr.next;
                            } 
                            return false;
                        }

Time complexity : O(n)
Space Complexity : O(n)

🔵 Optimized Approach (Floyd’s Cycle Detection – Tortoise & Hare)

Idea : Use two pointers
- slow pointer moves 1 step
- fast pointer moves 2 step
- if there is a cycle, fast and slow will eventually meet
- if no cycle -> fast will reach null

                        public boolean hasCycle(ListNode head){
                            if(head == null || head.next == null) return false;

                            ListNode slow = head;
                            ListNode fast = head;

                            while(fast != null && fast.next != null){
                                slow = slow.next;
                                fast = fast.next.next;

                                if(slow == fast) return true;
                            }
                            return false;
                        }

Time complexity : O(n)
Space complecity : O(1)
