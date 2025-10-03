Leetcode 21

Problem : Given two sorted linked lists list1 and list2
Merge them into one sorted linkedlist and return its head

Example : 
Input : list1 = [1 -> 2 -> 4] list2 = [1 ->3 -> 4]
Output : [1-> 1-> 2-> 3-> 4-> 4]

Input : list1 = [], list2 = [0]
Output : [0]


🟢 Brute Force Approach

Idea : 
1. traverse both the lists and store all values in an array
2. sort the array
3. create a new linkedlist from sorted values

                    public ListNode mergeTwoLists(ListNode list1, ListNode list2){
                        List<Integer> values = new ArrayList<>();

                        while (list1 != null){
                            values.add(list1.val);
                            list1 = list1.next;
                        }
                        while (list2 != null){
                            values.add(list2.val);
                            list2 = list2.next;
                        }

                        Collections.sort(values);

                        ListNode dummy = new ListNode(-1);
                        ListNode curr = dummy;
                        for(int val : values){
                            curr.next = new ListNode(val);
                            curr = curr.next;
                        }
                        return dummy.next;
                    }
Time complexity : O(m + n)log(m+n)
Space complexity : O(m+n)

🔵 Optimized Approach (Two Pointers – In-place Merge)

Idea :
- Both lists are already sorted
- Use two pointers to merge them like merge step in merge sort
- No extra sorting required

                    public ListNode mergeTwoLists(ListNode list1, ListNode list2){
                        ListNode dummy = new ListNode(-1);
                        ListNode tail = dummy;

                        while(list1 != null && list2 != null){
                            if(list.val < list2.val){
                                tail.next = list1;
                            }else{
                                tail.next = list2;
                                list2 = list2.next;
                            }
                            tail = tail.next;
                        }

                        if (list1 != null) tail.next = list1;
                        if (list2 != null) tail.next = list2;

                        return dummy.next;
                    }
Time Complexity : O(m + n)
Space complexity : O(1)

🔵 Recursive Version -> More Efficient

                    public ListNode mergeTwoLists(ListNode list1, ListNode list2){
                        if(list1 == null) return list2;
                        if(list2 == null) return list1;

                        if(list1.val < list2.val){
                            list.next = mergeTwoLists(list1.next, list2);
                            return list1;
                        }else{
                            list2.next = mergeTwoLists(list1, list2.next);
                            return list2;
                        }
                    }
