### 56. 合并区间
```python
class Solution:
    def merge(self, intervals: list[list[int]]) -> list[list[int]]:
        # 按照第一个元素排序，用什么数据类型？
        # end1>= start2就合并，重新定义开头=start1结尾=end2
        lenth = len(intervals)
        ans = []
        intervals.sort(key=lambda x: x[0])# 这种很少用
        # for i in range(lenth):
        #     for j in range(0,lenth - i - 1):
        #         if intervals[j][0] > intervals[j+1][0]:
        #             intervals[j], intervals[j+1] =intervals[j+1], intervals[j]
        for i, sublist in enumerate(intervals[:-1]):
            if sublist[1] >= intervals[i+1][0]:
                intervals[i+1][0] = intervals[i][0]
                intervals[i+1][1] = max(intervals[i+1][1],sublist[1])
            else:
                ans.append(sublist)
        ans.append(intervals[-1])
        return ans
```

### 189. 轮转数组
```python
class Solution:
    def rotate(self, nums: list[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        # k对len求余数
        # [len-k:] [0,len-k]
        k = k%len(nums)
        n= len(nums)
        # a = nums[len(nums)-k:]
        # b = nums[0:len(nums)-k]
        # nums[0:k]=a
        # nums[k:] = b
        nums[:] = nums[n-k:] + nums[:n-k]
```
空间o(1)
```python
class Solution:
    def rotate(self, nums: list[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        def reverse(i: int, j: int) -> None:
            while i < j:
                nums[i], nums[j] = nums[j], nums[i]
                i += 1
                j -= 1
        n = len(nums)
        k %= n  # 轮转 k 次等同于轮转 k % n 次
        reverse(0, n - 1)
        reverse(0, k - 1)
        reverse(k, n - 1)
```