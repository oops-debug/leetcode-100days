# 零、常用枚举技巧
## 思维拓展
### 3917. 统计下标的相反奇偶性得分 做到 O(n)
枚举左，维护右，但是从右开始枚举
```python
class Solution(object):
    def countOppositeParity(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        n = len(nums)
        cnt = [0]*2
        ans = [0]*n
        for i in range(n-1,-1,-1):
            x = nums[i]%2
            ans[i] = cnt[1-x]
            cnt[x] += 1
        return ans
```