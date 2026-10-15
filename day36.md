### 21.合并两个有序链表
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def mergeTwoLists(self, list1: ListNode | None, list2: ListNode | None) -> ListNode | None:
        # 如果两个节点都不空
        # 比大小，小的放下然后next
        # dummy = ListNode()
        # cur = dummy
        # while list1 and list2:
        #     if list1.val>=list2.val:
        #         cur.next = list2
        #         list2 = list2.next
        #     else:
        #         cur.next = list1
        #         list1 = list1.next
        #     cur = cur.next
        # if list1:
        #     cur.next = list1
        # if list2:
        #     cur.next = list2
        # return dummy.next
        if list1 is None: return list2
        if list2 is None: return list1
        if list1.val < list2.val:
            list1.next = self.mergeTwoLists(list1.next, list2)
            return list1
        else:
            list2.next = self.mergeTwoLists(list1, list2.next)
            return list2
```