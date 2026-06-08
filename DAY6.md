# 常用枚举技巧
## 枚举中间
### 2909. 元素和最小的山形三元组 II
维护一个后缀的最小值的列表，前缀直接更新
```python
class Solution(object):
    def minimumSum(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        suf = [0] * n
        suf[-1] = nums[-1]  # 后缀最小值
        for i in range(n - 2, 1, -1):
            suf[i] = min(suf[i + 1], nums[i])
        print(suf)
        ans = float("inf")
        minleft = nums[0]
        for i in range(1,len(nums)-1):
            minright = suf[i+1]
            if nums[i] > minleft and nums[i] > minright:
                ans = min(ans,nums[i]+minleft+minright)
            minleft = min(nums[i],minleft)
        return ans if ans != float('inf') else -1
```