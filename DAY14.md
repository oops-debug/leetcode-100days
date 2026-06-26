### 1371.每个元音包含偶数次的最长子字符串
```python
class Solution:
    def findTheLongestSubstring(self, s: str) -> int:
        st = {'a','e','i','o','u'}
        ans = 0
        pos = {0:-1}# 这里空前缀要放到-1的地方
        bit = 0
        for i, c in enumerate(s):
            if c in st:
                bit ^= 1 << (ord(c)-ord('a'))
            if bit in pos:
                ans = max(ans,i-pos[bit])
            else:
                pos[bit] = i
        return ans
```

### 2389. 和有限的最长子序列
```python
class Solution:
    def answerQueries(self, nums: List[int], queries: List[int]) -> List[int]:
        nums = sorted(nums)
        prifnums = list(accumulate(nums,initial=0))
        ans = []
        print(prifnums)
        for query in queries:
            ans.append(bisect_right(prifnums,query)-1)
        return ans
```

### 3709. 设计考试分数记录器 
```python
class ExamTracker:

    def __init__(self):
        self.times = []
        self.pre_sum = [0]

    def record(self, time: int, score: int) -> None:
        self.times.append(time)
        self.pre_sum.append(self.pre_sum[-1]+score)
    def totalScore(self, startTime: int, endTime: int) -> int:
        left = bisect_left(self.times,startTime)
        right = bisect_right(self.times,endTime)
        return self.pre_sum[right] - self.pre_sum[left]


# Your ExamTracker object will be instantiated and called as such:
# obj = ExamTracker()
# obj.record(time,score)
# param_2 = obj.totalScore(startTime,endTime)
```