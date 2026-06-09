# 常用枚举技巧
## 枚举中间
### 447. 回旋镖的数量
避免了重复计算：但是时间更长了，维护全局哈希表变长，不如一次维护一个
```python
class Solution(object):
    def numberOfBoomerangs(self, points):
        """
        :type points: List[List[int]]
        :rtype: int
        """
        cnt = defaultdict(int)
        ans = 0
        for i in range(len(points)-1):
            for j in range(i+1,len(points)):
                d = (points[i][0]-points[j][0])**2+(points[i][1]-points[j][1])**2
                ans += cnt[(i,d)]*2
                cnt[(i,d)] += 1 
                ans += cnt[(j,d)]*2
                cnt[(j,d)] += 1
        return ans

```
```python
class Solution(object):
    def numberOfBoomerangs(self, points):
        """
        :type points: List[List[int]]
        :rtype: int
        """
        ans = 0
        for x1,y1 in points:   
            cnt = defaultdict(int)     
            for x2,y2 in points:
                d = (x1-x2)**2+(y1-y2)**2
                ans += cnt[d]*2
                cnt[d]+=1
        return ans

```
### 456. 132
```python

class Solution(object):
    def find132pattern(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        n = len(nums)
# 左侧最小值
        left_min = nums[0]
        # 右侧所有元素
        right_all = SortedList(nums[2:])
        
        for j in range(1, n - 1):
            if left_min < nums[j]:
                index = right_all.bisect_right(left_min)
                if index < len(right_all) and right_all[index] < nums[j]:
                    return True
            left_min = min(left_min, nums[j])
            right_all.remove(nums[j + 1])

        return False
```
## 0.3 遍历对角线
### 3446. 按对角线进行矩阵排序
```python
class Solution(object):
    def sortMatrix(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: List[List[int]]
        """
        n = len(grid)
        m = len(grid[0])
        for k in range(1,m+n):
            min_i = max(n-k,0)
            max_i = min(m+n-1-k,n-1)
            a = [grid[k+i-n][i] for i in range(min_i,max_i+1)]
            a.sort(reverse = min_i==0)
            for i,val in zip(range(min_i,max_i+1),a):
                grid[k+i-n][i] = val
        return grid
```

