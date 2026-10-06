### 48.旋转图像
```python
class Solution:
    def rotate(self, matrix: list[list[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        # 顺时针=先倒序，后转置
        matrix[:] = list(zip(*matrix[::-1]))
```

### 240. 搜索二维矩阵 II
```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        m, n = len(matrix), len(matrix[0])
        i, j = 0, n-1
        # 右上角是第一行最大，最后一列最小
        # 如果找到就返回
        while i < m and j >= 0:
            if matrix[i][j] == target:
                return True
        # 如果target大于matrix[0][n-1]第一行删除
            if matrix[i][j] < target:
                i += 1
            else:
                j -= 1
        return False
        # 否则最后一列删除
```
### 160. 相交链表
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        p, q = headA, headB
        while p is not q:
            p = p.next if p else headB
            q = q.next if q else headA
        return p
```