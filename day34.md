### 234.回文链表
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    # def middleNode(self, head: ListNode | None) -> ListNode | None:
    #     slow = fast = head
    #     while fast and fast.next:
    #         slow = slow.next
    #         fast = fast.next.next
    #     return slow
    # def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
    #     pre, cur = None, head
    #     while cur:
    #         nxt = cur.next
    #         cur.next = pre
    #         pre = cur
    #         cur = nxt
    #     return pre
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        # left = head

        # def is_pal(right: Optional[ListNode]) -> bool:
        #     # 「递」，先把 right 移到链表末尾
        #     if right.next and not is_pal(right.next):
        #         return False
        #     # 「归」的过程就是在从右到左遍历链表
        #     nonlocal left
        #     if left.val != right.val:
        #         return False
        #     left = left.next  # left 往右走
        #     return True  # 归，right 会往左走

        # return is_pal(head)

        # mid = self.middleNode(head)
        # head2 = self.reverseList(mid)
        # while head2:
        #     if head.val != head2.val:
        #         return False
        #     head = head.next
        #     head2 = head2.next
        # return True

        slow = fast = head
        pre = None
        cur = head
        while fast != None and fast.next != None:
            fast = fast.next.next
            cur = slow.next
            slow.next = pre
            pre = slow
            slow = cur
        if fast:    
            slow = slow.next

        while slow != None:
            if pre.val != slow.val:
                return False
            slow = slow.next
            pre = pre.next
        return True
        
```

### 70.爬楼梯
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        @cache
        def dfs(i:int):
            if i<= 1:
                return 1
            return dfs(i-1) + dfs(i-2)
        return dfs(n)
```

### 1143.最长公共子序列
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        n,m = len(text1),len(text2)
        @cache
        def dfs(i,j):
            if i < 0 or j < 0:
                return 0
            if text1[i] == text2[j]:
                return dfs(i-1,j-1) + 1
            return max(dfs(i-1,j),dfs(i,j-1))
        return dfs(n-1,m-1)