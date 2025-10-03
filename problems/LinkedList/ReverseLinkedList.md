Leetcode 206

Problem : You are given the head of a singly linkedlist
Reverse the list, so that last node becomes the head
Return the new head

Example :
Input : 1 -> 2 -> 3 -> 4 -> 5
Output : 5 ->4 -> 3 -> 2 -> 1

Approach 1 : Brute Force (Recursive)

Idea : If you reach end, return the last node as the new head
While unwinding recursion, flip the next pointers

Recursive

                    public ListNode reverseList(ListNode head){
                        //base case :empty list or single node
                        if(head == null || head.next == null) return head;

                        //reverse rest of the list
                        ListNode newHead = reverseList(head.next);

                        //flip the link
                        head.next.next = head;
                        head.next = null;

                        return newHead;
                    }

Time complexity : O(n)
Space complexity : O(n)

⚡ Approach 2: Optimized Iterative (Two Pointers)

Idea : Maintain three pointers : prev, curr, next
Traverse the list and reverse pointers one by one

Code (Iterative)

public ListNode reverseList(ListNode head){
    ListNode prev = null;
    ListNode curr = head;

    while (curr != null){
        ListNode nextNode = curr.next;      //save next
        curr.next = prev;                   //reverse link
        prev = curr;                        //move prev forward
        curr = nextNode;                    //move curr forward
    }
    return prev;
}
Time Complexity : O(n)
Space Complexity :O(1)
