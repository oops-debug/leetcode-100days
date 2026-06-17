### 1310. 子数组异或查询
```python
class Solution(object):
    def xorQueries(self, arr, queries):
        """
        :type arr: List[int]
        :type queries: List[List[int]]
        :rtype: List[int]
        """
        n = len(arr)     
        arr1 = [0]*(n+1)
        ans = []
        for i in range(n):
            arr1[i+1] += arr1[i]^arr[i]
        for query in queries:
            ans.append(arr1[query[1]+1]^arr1[query[0]])
        return ans
```

### 3152. 特殊数组 II

```python
class Solution(object):
    def isArraySpecial(self, nums, queries):
        n = len(nums)
        s = [0] * n

        for i in range(n - 1):
            # 不是相等也要继承
            s[i + 1] = s[i]
            if nums[i] % 2 == nums[i + 1] % 2:
                s[i + 1] += 1
        # 第一位保持为0
        ans = []
        for from_, to in queries:
            ans.append(s[to] == s[from_])
        return ans
```

### 560. 和为 K 的子数组

```python
# 滑动窗口使用需要考虑前缀和的单调性：原始数组不能有负数
# 如果有负数使用前缀和
# 这道题：前缀和+哈希表（来源于两数之和）
class Solution(object):
    def subarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        n = len(nums)
        s = [0]*(n+1)
        for i,x in enumerate(nums):
            s[i + 1] = s[i] + x
        cnt = defaultdict(int)
        ans = 0
        for sj in s:
            ans += cnt[sj - k]
            cnt[sj] += 1
        return ans
class Solution(object):
    def subarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        n = len(nums)
        cnt = defaultdict(int)
        cnt[0] = 1# 单独处理：从0开始的情况
        ans = s = 0
        for x in nums:
            s += x
            ans += cnt[s-k]
            cnt[s] += 1
        return ans
# 无需初始化
class Solution(object):
    def subarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        n = len(nums)
        cnt = defaultdict(int)
        # cnt[0] = 1
        # 单独处理：从0开始的情况
        ans = s = 0
        for x in nums:
            # 在同一轮循环中先把是s[i-1]加入哈希，再更新答案
            cnt[s] += 1
            s += x
            ans += cnt[s-k]
        return ans
```