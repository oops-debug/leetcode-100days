## 子串
### 560.和为k的子数组
和两数之和有点像，一个是两数+哈希，现在是前缀的差+哈希
```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        cnt = defaultdict(int)
        cnt[0] += 1
        prenum = 0
        ans = 0
        for c in nums:
            prenum += c
            ans += cnt[prenum-k]
            cnt[prenum] += 1
        return ans
```
### 239.滑动窗口最大值
```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        ans = [0]*(len(nums)-k+1)
        q = deque()
        for i, x in enumerate(nums):
            while q and nums[q[-1]]<= x:# 遍历到一个新的数，那么之前比他小的就可以删掉了，
                q.pop()
            q.append(i)
            left = i - k + 1
            if q[0] < left:
                q.popleft()
            if left >= 0:
                ans[left] = nums[q[0]]

        return ans
```