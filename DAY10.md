### 303. 区域和检索 - 数组不可变

```python
class NumArray(object):
    # 前缀和
    def __init__(self, nums):
        """
        :type nums: List[int]
        """
        s = [0]*(len(nums)+1)
        for i,x in enumerate(nums):
            s[i+1] = s[i]+x
        self.s = s

    def sumRange(self, left, right):
        """
        :type left: int
        :type right: int
        :rtype: int
        """
        ans = 0
        for i in range(left,right+1):
            ans = self.s[right+1] - self.s[left]

        return ans


# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(left,right)
```
### 3427. 变长子数组求和
* 还有一种差分数组法
```python
class Solution(object):
    def subarraySum(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        ans = 0
        s = [0]*(len(nums)+1)
        for i,x in enumerate(nums):
            s[i+1] = s[i] + x
        for i,x in enumerate(nums):
            start = max(0, i-x)
            ans += s[i+1] - s[start]
        return ans
```

### 2559. 统计范围内的元音字符串数

```python
class Solution(object):
    def vowelStrings(self, words, queries):
        """
        :type words: List[str]
        :type queries: List[List[int]]
        :rtype: List[int]
        """
        n = len(words)
        nums= [0]*(n+1)
        ans = []
        a = set("aeiou")
        for i,x in enumerate(words):
            nums[i+1] = nums[i] + 1 if x[0] in a and x[-1] in a else nums[i]
        for x in queries:
            ans.append(nums[x[1]+1]-nums[x[0]])
        return ans

```