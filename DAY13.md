### 3364. 最小正和子数组
```python
class Solution:
    def minimumSumSubarray(self, nums: List[int], l: int, r: int) -> int:
        ans = inf
        s = list(accumulate(nums,initial=0))
        sl = SortedList()
        for j in range(l,len(nums)+1):
            sl.add(s[j-l])
            k = sl.bisect_left(s[j])
            if k:
                ans = min(ans,s[j]-sl[k-1])
            if j >= r:
                sl.remove(s[j-r])
        return -1 if ans == inf else ans
```

### 363. 矩形区域不超过 K 的最大数值和
```python
class Solution:
    def maxSumSubmatrix(self, matrix: List[List[int]], k: int) -> int:
        m = len(matrix)
        n = len(matrix[0])
        ans = float('-inf')
        for top in range(m):
            colm = [0] * n
            for bottom in range(top,m):
                for j in range(n):
                    colm[j] += matrix[bottom][j]
                colpri = list(accumulate(colm,initial = 0))
                sm = SortedList()
                s = 0
                for sj in colpri:
                    i = sm.bisect_left(sj-k)
                    if i != len(sm):
                        ans = max(ans,sj - sm[i])
                    sm.add(sj)
        return ans
```
### 2602. 使数组元素全部相等的最少操作次数
```python
class Solution:
    def minOperations(self, nums: List[int], queries: List[int]) -> List[int]:
        n = len(nums)
        nums.sort()
        s = list(accumulate(nums,initial=0))
        ans = []
        for q in queries:
            j = bisect_left(nums,q)
            left = q*j - s[j]
            right = s[n] - s[j] - (n - j)*q
            ans.append(left+right)
        return ans
```
### 1685. 有序数组中差绝对值之和

```python
class Solution:
    def getSumAbsoluteDifferences(self, nums: List[int]) -> List[int]:
        numsPri = list(accumulate(nums,initial=0))
        last = numsPri[-1]
        n = len(nums)
        result = []
        for i in range(n):
            numPri = numsPri[i]
            this = nums[i]
            result.append(last-2*numPri+2*i*this-n*this)
        return result
```

### 2615. 等值距离和
方法1
```python
class Solution:
    def distance(self, nums: List[int]) -> List[int]:
        groups = defaultdict(list)
        for i, x in enumerate(nums):
            groups[x].append(i)
        ans = [0]*len(nums)
        for a in groups.values():
            n = len(a)
            s = list(accumulate(a,initial=0))
            for j,target in enumerate(a):
                left = target*j -s[j]
                right = s[n] - s[j] - target*(n-j)
                ans[target] = left + right
        return ans
```
方法2
```python
class Solution:
    def distance(self, nums: List[int]) -> List[int]:
        groups = defaultdict(list)
        for i, x in enumerate(nums):
            groups[x].append(i)  # 相同元素分到同一组，记录下标
        ans = [0] * len(nums)
        for a in groups.values():
            n = len(a)
            s = sum(x - a[0] for x in a)  # a[0] 到其它下标的距离之和
            ans[a[0]] = s
            for i in range(1, n):
                # 从计算 a[i-1] 到计算 a[i]，考虑 s 增加了多少
                s += (i * 2 - n) * (a[i] - a[i - 1])
                ans[a[i]] = s
        return ans
```


### 2602. 使数组元素全部相等的最少操作次数
```python
class Solution:
    def minOperations(self, nums: List[int], queries: List[int]) -> List[int]:
        n = len(nums)
        nums.sort()
        s = list(accumulate(nums,initial=0))
        ans = []
        for q in queries:
            j = bisect_left(nums,q)
            left = q*j - s[j]
            right = s[n] - s[j] - (n - j)*q
            ans.append(left+right)
        return ans
```
### 1177. 构建回文串检测
```python
class Solution:
    def canMakePaliQueries(self, s: str, queries: List[List[int]]) -> List[bool]:
        sum = [0]
        for c in s:
            bit = 1 << (ord(c) - ord('a'))
            sum.append(sum[-1]^bit)# ^ 异或符号求奇数个数
        ans = []
        for left, right, k in queries:
            m = (sum[left] ^ sum[right+1]).bit_count()
            ans.append(m//2<=k)
        return ans
```
