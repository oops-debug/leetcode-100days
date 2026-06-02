# 零、常用枚举技巧
## 进阶
### 2748. 美丽下标对的数目
暴力解法：n*(n+logC)
```python
from fractions import gcd
class Solution(object):
    def countBeautifulPairs(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        ans = 0
        for i in range(len(nums)-1):
            while nums[i]>=10:
                nums[i]//= 10
            for num1 in nums[:i+1]:
                if gcd(num1,nums[i+1]%10) == 1:
                    ans += 1
        return ans
```

非暴力,因为数量少，直接开十个数的数组来记录:n*(10+logC)

```python
from fractions import gcd
class Solution(object):
    def countBeautifulPairs(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        ans = 0
        cnt = [0]*10
        for x in nums:
            for y,c in enumerate(cnt):
                if c and gcd(y,x%10)==1:
                    ans += c
            while x>=10:
                x//=10
            cnt[x] += 1
        return ans
```

### 2506.统计相似字符串对的数目

暴力解法：n(n+m)
```python
class Solution(object):
    def similarPairs(self, words):
        """
        :type words: List[str]
        :rtype: int
        """
        ans = 0
        wordset = []
        for i,word in enumerate(words):
            cnt = set(word)
            wordset.append(cnt)
            for cnt1 in wordset[:i]:
                ans += 1 if cnt1 == cnt else 0
        return ans
```

先变成集合再查哈希表，时间复杂度：L 所有word加起来的长度
```python
class Solution(object):
    def similarPairs(self, words):
        """
        :type words: List[str]
        :rtype: int
        """
        ans = 0
        cnt = defaultdict(int)
        for word in words:
            word = ''.join(sorted(set(s)))
            ans += cnt[s] # 先更新ans再加，符合（2-1）+（3-1）......
            cnt[s] += 1
        return ans
```

独热编码

```python
class Solution(object):
    def similarPairs(self, words):
        """
        :type words: List[str]
        :rtype: int
        """
        ans = 0
        cnt = defaultdict(int)
        for word in words:
            mask = 0
            for c in word:
                mask |= 1 << (ord(c)-ord('a'))
            ans += cnt[mask]
            cnt[mask] += 1
        return ans
```

### 2874.有序三元组中的最大值
暴力：超时
```python
class Solution(object):
    def maximumTripletValue(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if sorted(nums) == nums:
            return 0
        ans = 0
        for k in range(2,len(nums)):
            for j in range(1,k):
                for i in range(0,j):
                    ans =max((nums[i]-nums[j])*nums[k],ans) 
        return ans
```

枚举j

```python
class Solution(object):
    def maximumTripletValue(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # 先计算后缀最大值
        ans = 0
        n = len(nums)
        sufMax = [0]*(n+1)# 会取到n+1
        preMax = nums[0]
        for i in range(n - 1, 1, -1):
            sufMax[i] = max(sufMax[i+1],nums[i])
        for j in range(1,n-1):
            ans = max((preMax-nums[j])*sufMax[j+1],ans)
            preMax = max(preMax,nums[j])
        return ans
```

枚举K

```python
class Solution(object):
    def maximumTripletValue(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        maxdiff = ans = premax = 0
        # 分析依赖关系
        for k in nums:
            ans = max(ans,maxdiff*k)
            maxdiff = max(maxdiff,premax-k)
            premax = max(premax,k)
        return ans
```
