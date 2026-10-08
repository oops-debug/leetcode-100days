### 206.反转链表
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: ListNode | None) -> ListNode | None:
        # 如果第一个就空，或者head.next空就说明递到了最后一个
        if head is None or head.next is None:
            return head
        # 返回尾节点
        rev_head = self.reverseList(head.next)
        # 递到末尾
        # 接下来是返回【归】
        tail = head.next
        tail.next = head
        head.next = None
        return rev_head
class Solution:
    def reverseList(self, head: ListNode | None) -> ListNode | None:
        # 如果第一个就空，或者head.next空就说明递到了最后一个
        pre = None # 去环 
        cur = head
        while cur:
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        return pre
```