```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next


class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        # Remove any empty lists from the input
        # This helps us avoid dealing with None values later
        lists = [lst for lst in lists if lst]
        
        # If there are no non-empty lists, return None
        if not lists:
            return None
        
        # Create a min-heap
        # We'll use this to efficiently get the smallest node at each step
        heap = []
        
        # Populate the heap with the first node from each list
        # We push tuples: (node.val, list_index, node)
        # - node.val is used for heap ordering
        # - list_index is used to identify which list the node came from
        # - node is the actual ListNode object
        for i, node in enumerate(lists):
            heapq.heappush(heap, (node.val, i, node))
        
        # Create a dummy node for the result
        # This simplifies the list building process as we don't need to handle the head separately
        dummy = ListNode(0)
        current = dummy
        
        # Continue while there are nodes in the heap
        while heap:
            # Pop the smallest node from the heap
            val, i, node = heapq.heappop(heap)
            
            # Add this node to our result list
            current.next = node
            current = current.next
            
            # If this node has a next node, push it onto the heap
            if node.next:
                heapq.heappush(heap, (node.next.val, i, node.next))
        
        # Return the head of the merged list
        # (remember, dummy.next is the actual head)
        return dummy.next
```