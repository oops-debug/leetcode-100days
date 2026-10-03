### 238. 除了自身以外数组的乘积
少遍历一次+空间o(1)
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        pre = [1] * n
        for i in range(1,n):
            pre[i] = pre[i-1] * nums[i-1]
        suf = nums[-1]
        for i in range(n-2,-1,-1):
            pre[i] *= suf
            suf *= nums[i]
        return pre
```
### 41. 缺失的第一个正数
```python
class Solution:
    def firstMissingPositive(self, nums: list[int]) -> int:
        # 如果学号范围在[1,n],但是真的座位上没有这个学号的 学生
        # 就交换nums[i]和nums[j]
        n = len(nums)
        for i in range(n):
            while 1<= nums[i] <= n and nums[nums[i]-1] != nums[i]:
                j = nums[i] - 1
                nums[i], nums[j] = nums[j], nums[i]
                # 找第一个不匹配的
        for i in range(n):
            if nums[i] != i+1:
                return i+1 
        return n+1
```