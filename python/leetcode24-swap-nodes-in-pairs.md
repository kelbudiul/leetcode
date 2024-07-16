```python
# Definition for singly-linked list.

# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:

        if not head:
            return None

        if not head.next:
            return head

        dummy = ListNode(0)
        prev = dummy
        dummy = head.next

        while head and head.next:
            first = head
            second = head.next
  
            prev.next = second
            first.next = second.next
            second.next = first

            prev = first
            head = first.next

        return dummy
```