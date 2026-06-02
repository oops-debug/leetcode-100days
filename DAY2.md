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
