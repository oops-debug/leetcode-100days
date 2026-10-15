### 2.两数相加
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode | None, l2: ListNode | None,carry=0) -> ListNode | None:
        # if l1 is None and l2 is None and carry == 0:
        #     return None
        
        # s = carry
        # if l1:
        #     s += l1.val
        #     l1 = l1.next
        # if l2:
        #     s += l2.val
        #     l2 = l2.next
        
        # return ListNode(s%10, self.addTwoNumbers(l1,l2,s//10))
        # 迭代法
        cur = dummy = ListNode()
        carry = 0
        while l1 or l2 or carry:
            s = carry
            if l1:
                s += l1.val
                l1 = l1.next
            if l2:
                s += l2.val
                l2 = l2.next
            cur.next = ListNode(s%10)
            carry = s//10
            cur = cur.next
        return dummy.next
        
```