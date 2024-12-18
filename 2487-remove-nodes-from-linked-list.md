# 2487. Remove Nodes From Linked List

https://leetcode.com/problems/remove-nodes-from-linked-list/description

![Screenshot 2024-05-06 at 1.49.30 PM.png](https://assets.leetcode.com/users/images/0d80e930-79ff-411b-9361-b2c6246e6d1c_1715028615.2593303.png)

# Intuition

Recursion is not a good option because the max list length is too long.
Can either reverse the linked list to make the problem easier, or read the list into some other data structure to determine which nodes to delete.

# Approach

1. Implement function to reverse the linked list in-place.
2. Implement loop to traverse the reversed list. Keep track of the greatest value encountered so far, and delete any node that is less than that value.

# Complexity

- Time complexity:
  $$O(n)$$ Traverse list 3x: reversing, deleting nodes, and reversing back.

- Space complexity:
  $$O(1)$$ List is modified in-place.

# Code

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
from collections import deque
class Solution:
    def removeNodes(self, head: Optional[ListNode]) -> Optional[ListNode]:
        def reverseLinkedList(head: Optional[ListNode]) -> Optional[ListNode]:
            prev, curr, nxt = None, head, head.next
            while curr:
                nxt = curr.next
                curr.next = prev
                prev = curr
                curr = nxt
            return prev
        head = reverseLinkedList(head)
        prev, curr, greatest = ListNode(next=head), head, head.val
        while curr:
            if curr.val < greatest:
                prev.next = curr.next
            else:
                greatest = curr.val
                prev = prev.next
            curr = curr.next
        return reverseLinkedList(head)
```
