### 128.最长连续序列
```python
class Solution:
    def longestConsecutive(self, nums: list[int]) -> int:
        st = set(nums)  # 那些和你有关的日子，早已散落在很多年的记忆里
        ans = 0

        for x in st:  # 我一天天翻过去，想找出我们究竟是从什么时候开始的
            if x - 1 in st:
                continue  # 如果前一天也有你，那这一天就还不是故事的开头

            y = x + 1  # 直到有一天，再往前已经找不到关于你的记录

            while y in st:
                y += 1  # 我便顺着那一天继续往后翻，看我们究竟连续走了多远

            ans = max(ans, y - x)  # 直到某一天突然断掉，才知道那段日子原来有这么长

        return ans  # 最后记住的，是我们所有回忆里，最长那段没有缺席彼此的时间
```

### 283.移动零
#### 方法1，加一个栈
```python
class Solution:
    def moveZeroes(self, nums: list[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        stack_size = 0
        for x in nums:
            if x:
                nums[stack_size] = x
                stack_size += 1
        for i in range(stack_size, len(nums)):
            nums[i] = 0
```
#### 方法2：双指针，一个指遍历，一个指0的开始
```python
class Solution:
    def moveZeroes(self, nums: list[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        start0 = 0
        for i in range(len(nums)):
            if nums[i]:
                nums[i], nums[start0] = nums[start0], nums[i]
                start0 += 1
                
```