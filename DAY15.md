### 3919. 在下标间移动的最小代价
```python
class Solution:
    def minCost(self, nums: list[int], queries: list[list[int]]) -> list[int]:
        n = len(nums)
        sum_l = [0]*n
        sum_r = [0]*n
        # 两端的处理
        # 0 -> i 
        for i in range(1,n):
            #   i-1 -> i从左到右 
            if i>1 and nums[i-1] - nums[i-2] <= nums[i] - nums[i-1]:
                cost = nums[i] - nums[i-1]
            else:
                cost = 1
            sum_l[i] = cost + sum_l[i-1]
            # 从右往左i->i-1
            if i< n-1 and nums[i] - nums[i-1] > nums[i+1] - nums[i]:
                cost = nums[i] - nums[i-1]
            else:
                cost = 1
            sum_r[i] = cost + sum_r[i-1]

        ans = [0]*len(queries)
        for i,q in enumerate(queries):
            l,r = q
            if l<r:
                ans[i] = sum_l[r] - sum_l[l]
            else:
                ans[i] = sum_r[l] - sum_r[r]
        return ans
```

## 1.6 二维前缀和

### 304. 二维区域和检索 - 矩阵不可变
```python
class NumMatrix:

    def __init__(self, matrix: List[List[int]]):
        m, n = len(matrix),len(matrix[0])
        s = [[0]*(n+1) for _ in range(m+1)]
        for i, row in enumerate(matrix):
            for j, x in enumerate(row):
                s[i+1][j+1] = s[i+1][j] + s[i][j+1] - s[i][j] + x
        self.s = s

    def sumRegion(self, r1: int, c1: int, r2: int, c2: int) -> int:
        s = self.s
        return s[r2+1][c2+1] - s[r2+1][c1] - s[r1][c2+1] + s[r1][c1]
# Your NumMatrix object will be instantiated and called as such:
# obj = NumMatrix(matrix)
# param_1 = obj.sumRegion(row1,col1,row2,col2)
```

### 1314. 矩阵区域和
```python
class Solution:
    def matrixBlockSum(self, mat: List[List[int]], K: int) -> List[List[int]]:
        m, n = len(mat), len(mat[0])
        P = [[0]*(n+1) for _ in range(m+1)]
        for i in range(1,m+1):
            for j in range(1,n+1):
                P[i][j] = P[i-1][j] + P[i][j-1] - P[i-1][j-1] + mat[i-1][j-1]
        ans = [[0]*n for _ in range(m)]
        def get(x,y):
            x = max(min(x,m),0)
            y = max(min(y,n),0)
            return P[x][y]
        for i in range(m):
            for j in range(n):
                ans[i][j] = get(i + K + 1, j + K + 1) - get(i - K, j + K + 1) - get(i + K + 1, j - K) + get(i - K, j - K)
        return ans
```

### 3070. 元素和小于等于 k 的子矩阵的数目
```python
class Solution:
    def countSubmatrices(self, grid: List[List[int]], k: int) -> int:
        m, n = len(grid), len(grid[0])
        s = [[0]*(n+1) for _ in range(m+1)]
        ans = 0
        for i, row in enumerate(grid):
            for j, x in enumerate(row):
                s[i+1][j+1] = s[i+1][j] + s[i][j+1] - s[i][j] + x
                if s[i+1][j+1] <= k:
                    ans += 1
        return ans
```

### 1738. 找出第 K 大的异或坐标值
```python
class Solution:
    def kthLargestValue(self, matrix: List[List[int]], k: int) -> int:
        m, n = len(matrix),len(matrix[0])
        s = [[0]*(n+1) for _ in range(m+1)]
        ans = 0
        for i, row in enumerate(matrix):
            for j, x in enumerate(row):
                s[i+1][j+1] = s[i+1][j]^s[i][j+1]^s[i][j]^x
        return sorted(x for row in s[1:] for x in row[1:])[-k]
```
