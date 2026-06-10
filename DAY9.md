### 2711. 对角线上不同值的数量差

注意行列对应

```python
class Solution(object):
    def differenceOfDistinctValues(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: List[List[int]]
        """
        st = set()
        m = len(grid)
        n = len(grid[0])
        ans = [[0] * n for _ in range(m)]
        # k = r - c + n
        for k in range(1,m+n):
            # r = c + k - n
            # c = r + n - k
            min_c = max(0,n-k)
            max_c = min(n-1,m+n-1-k)
            st.clear()
            for c in range(min_c,max_c + 1):
                r = c + k - n
                ans[r][c] = len(st)
                st.add(grid[r][c])
            st.clear()
            for c in range(max_c,min_c-1,-1):
                r = c + k - n
                ans[r][c] = abs(len(st)-ans[r][c])
                st.add(grid[r][c])
        return ans
```
### 1329. 将矩阵按对角线排序
```python
class Solution(object):
    def diagonalSort(self, mat):
        """
        :type mat: List[List[int]]
        :rtype: List[List[int]]
        """
        # i - j + n = k
        # j = i + n - k
        # i = j+k-n
        n = len(mat[0])
        m = len(mat)
        for k in range(1,m+n-1):
            max_j = min(n-1,m + n -1 -k)
            min_j = max(0,n-k)
            print(max_j)
            a = [mat[j+k-n][j] for j in range(min_j,max_j+1)]
            a.sort()
            print(a)
            for j,val in zip(range(min_j,max_j+1),a):
                mat[j+k-n][j] = val
        return mat
```
### 498. 对角线遍历
```python
class Solution(object):
    def findDiagonalOrder(self, mat):
        """
        :type mat: List[List[int]]
        :rtype: List[int]
        """
        # i + j = k
        # j = k - i
        n = len(mat[0])
        m = len(mat)
        a = []
        for k in range(m+n-1):
            max_j = min(n-1,k)
            min_j = max(0,k-m+1)
            print(max_j)
            if k % 2 == 0:          
                for j in range(min_j,max_j+1):
                    a.append(mat[k - j][j] )
            else:
                for j in range(max_j, min_j - 1, -1):
                    a.append(mat[k - j][j])
        return a
```