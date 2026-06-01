# 零、常用枚举技巧
## 基础
### 1.两数之和
枚举右，维护左
```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        hashtable = {}
        for i, num in enumerate(nums):
            need = target - num
            if need in hashtable:
                return [hashtable[need],i]
            hashtable[num] = i
        return []
```

### 1512.好数对的数目
```python
class Solution(object):
    def numIdenticalPairs(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        hashtable = defaultdict(int)
        ans = 0
        for num in nums:
            ans += hashtable[num]
            hashtable[num] += 1
        return ans
```

### 2441.与对应负数同时存在的最大正数
```python
class Solution(object):
    def findMaxK(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        ans = -1
        s = set()# 只存key,不存VALUE
        for num in nums:
            if -num in s:
                ans = max(abs(num),ans)
            s.add(num)
        return ans
```

### 121.买卖股票最佳时机
简洁写法：枚举卖出价格，维护买入的最小值
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        minleft = prices[0]
        ans = 0
        for num in prices[1:]:
            ans = max(ans,num - minleft)
            minleft = min(minleft, num)
        return ans
```

### 2016.增量元素之间的最大差值
```python
class Solution(object):
    def maximumDifference(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        minleft = nums[0]
        ans = 0
        for num in nums[1:]:
            ans = max(ans,num - minleft)
            minleft = min(minleft,num)
        return ans or -1 # return ans if ans else -1
```
## 进阶
### 1010.总持续时间可被60整除
```python
class Solution(object):
    def numPairsDivisibleBy60(self, time):
        """
        :type time: List[int]
        :rtype: int
        """
        s = defaultdict(int)
        ans = 0
        for num in time:
            timeM = num % 60
            # if timeM == 0 :
            #     ans += s[0]
            # ans += s[60-timeM]
            ans += s[(60 - timeM) % 60] # 处理了可以整除的时候存进去的数=0的情况:本来会搜索60-timeM,现在搜索0,而其他数不变
            s[timeM] += 1
        return ans
```

### 3185.构成整天的下标对数组
```python
class Solution(object):
    def countCompleteDayPairs(self, hours):
        """
        :type hours: List[int]
        :rtype: int
        """
        # cnt = defaultdict(int)
        cnt = [0] * 24 # 连续确定的值用这个
        ans = 0
        for hour in hours:
            hourM = hour%24
            ans += cnt[(24-hourM)%24]
            cnt[hourM]+=1
        return ans
```
