### 3212. 统计 X 和 Y 频数相等的子矩阵数量
```python
class Solution:
    def numberOfSubmatrices(self, grid: List[List[str]]) -> int:
        m = len(grid)
        n = len(grid[0])
        x_num = [[0]*(n+1) for _ in range(m+1)]
        y_num = [[0]*(n+1) for _ in range(m+1)]
        ans = 0
        for i,row in enumerate(grid):
            for j, x in enumerate(row):
                # x_num[i+1][j+1] = x_num[i+1][j] + x_num[i][j+1] - x_num[i][j] + 1 if x == 'X' else x_num[i+1][j] + x_num[i][j+1] - x_num[i][j]
                # y_num[i+1][j+1] = y_num[i+1][j] + y_num[i][j+1] - y_num[i][j] + 1 if x == 'Y' else y_num[i+1][j] + y_num[i][j+1] - y_num[i][j]
                x_num[i+1][j+1] = x_num[i+1][j] + x_num[i][j+1] - x_num[i][j]
                y_num[i+1][j+1] = y_num[i+1][j] + y_num[i][j+1] - y_num[i][j]
                if x != '.':
                    x_num[i+1][j+1] += ord(x)&1
                    y_num[i+1][j+1] += ~ord(x)&1
                # 用位运算代替if判断
                if x_num[i+1][j+1] > 0 and x_num[i+1][j+1] == y_num[i+1][j+1]:
                    ans+=1
        return ans
```