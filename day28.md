### 76. 最小覆盖子串
```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        left = count = 0
        start = 0
        # need哈希统计需要的字符+对应的次数
        need = defaultdict(int)
        window = defaultdict(int)
        for c in t:
            need[c] += 1
        minLen = float('inf')
        # right不断右移，更新当前字母c，
        for right, c in enumerate(s):
            if c in need:
                window[c] += 1
                if window[c] == need[c]:
                    count += 1
            while count == len(need):
                # start = max(start,left)
                # minLen = min(right-left+1,minLen)
                if right - left + 1 < minLen:
                    start = left
                    minLen = right - left + 1
                if s[left] in need :
                    count -= 1 if window[s[left]] == need[s[left]] else 0# left
                    window[s[left]] -= 1
                left+=1
        return "" if minLen == float('inf') else s[start:start+minLen]
        # 如果c在need，count++，更新window
        # count == need.size就收缩left
        # left向右收缩
        # while s[left]在need中就右移直到遇到在need中,更新window
```

### 53. 最大子数组和
还有一种分治法/动态规划没有实现
```python
class Solution:
    def maxSubArray(self, nums: list[int]) -> int:
        sum = 0
        tmp = float('inf')# 保存前缀最小值
        ans = -float('inf')
        for num in nums:
            tmp = min(tmp,sum)
            sum += num
            ans = max(ans,sum-tmp) 
        return ans
```