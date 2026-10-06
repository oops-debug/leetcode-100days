### 73. 矩阵置零
```python
from collections import defaultdict
class Solution:
    def setZeroes(self, matrix: list[list[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        # m = len(matrix)
        # n = len(matrix[0])
        # row = defaultdict(int)
        # line = defaultdict(int)
        # # m存放第几行有0，n存放第几列有0
        # # 遍历遇到0就记录行和列
        # # 再次遍历，但凡行/列为0就解决
        # for i in range(m):
        #     for j in range(n):
        #         if matrix[i][j]==0:
        #             row[i] = 1
        #             line[j] = 1
        # for i in range(m):
        #     for j in range(n):
        #         if row[i] == 1 or line[j] == 1:
        #             matrix[i][j] = 0


        # row_has_zero = [0 in row for row in matrix]
        # col_has_zero = [0 in col for col in zip(*matrix)]

        # for i, row0 in enumerate(row_has_zero):
        #     for j, col0 in enumerate(col_has_zero):
        #         if row0 or col0:
        #             matrix[i][j] = 0

        # 不使用额外数组，第一行/列保存信息，那第一行的信息怎么办？用两个额外的数保存
        # m, n = len(matrix), len(matrix[0])
        # first_row_has_zero = 0 in matrix[0]
        # first_col_has_zero = any(row[0] == 0 for row in matrix)
        
        # for i in range(1, m):
        #     for j in range(1, n):
        #         if matrix[i][j] == 0:
        #             matrix[i][0] = 0
        #             matrix[0][j] = 0

        # for i in range(1, m):
        #     for j in range(1, n):
        #         if matrix[i][0] == 0 or matrix[0][j] == 0:
        #             matrix[i][j] = 0
        # if first_col_has_zero:
        #     for row in matrix:
        #         row[0] = 0
        # if first_row_has_zero:
        #     for j in range(n):
        #         matrix[0][j] = 0
        
        # 但是不用这么麻烦，用第一行记录每一列（包括第一列），那么第一行怎么办？直接用一个元素记录第一行
        m, n = len(matrix), len(matrix[0])
        first_row_has_zero = 0 in matrix[0]
        for i in range(1, m):
            for j in range(n):  # 如果第一列包含 0，那么 matrix[0][0] 会置为 0
                if matrix[i][j] == 0:
                    matrix[i][0] = matrix[0][j] = 0

        for i in range(1, m):
            for j in range(1, n):
                if matrix[i][0] == 0 or matrix[0][j] == 0:
                    matrix[i][j] = 0

        # 注意顺序，先改第一列，再改第一行（避免把 matrix[0][0] 从 1 改成 0 影响判断）
        if matrix[0][0] == 0:  # 替换原来的 first_col_has_zero
            for row in matrix:
                row[0] = 0

        if first_row_has_zero:
            for j in range(n):
                matrix[0][j] = 0

```
### 54. 螺旋矩阵
```python
# DIRS = (0, 1), (1, 0), (0, -1), (-1, 0)  # 右下左上
# class Solution:
#     def spiralOrder(self, matrix: list[list[int]]) -> list[int]:
#         m = len(matrix)
#         n = len(matrix[0])
#         size = m*n
#         ans = []
#         # 起点（0，-1）
#         i, j , di = 0, -1, 0
#         # 遍历ans<m*n
#         while len(ans) < size:
#             # 递增的规律 (0, 1), (1, 0), (0, -1), (-1, 0) 循环
#             dx, dy = DIRS[di]
#             for _ in range[n]:
#                 i += dx
#                 j += dy
#                 ans.append(matrix[i][j])
#             di = (di+1)%4
#             m, n = n, m-1
#         return ans
        
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        res = []
        while matrix:
            res.extend(matrix[0])
            matrix.pop(0)
            matrix = list(zip(*matrix))[::-1]
        return res
```