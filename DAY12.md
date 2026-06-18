### 930. 和相同的二元子数组
```python
class Solution(object):
    def numSubarraysWithSum(self, nums, goal):
        """
        :type nums: List[int]
        :type goal: int
        :rtype: int
        """
        # 遍历右，维护左
        sum2 = left2 = left = right = ans = sum1 = 0
        for right,x in enumerate(nums):
            sum1 += x
            sum2 += x
            while left <= right and sum1 >= goal:
                sum1 -= nums[left]
                left += 1
            while left2 <= right and sum2 > goal:
                sum2 -= nums[left2]
                left2 += 1
            ans += left - left2
        return ans
```

### 1524. 和为奇数的子数组数目

```python
class Solution(object):
    def numOfSubarrays(self, arr):
        """
        :type arr: List[int]
        :rtype: int
        """
        # 维护前缀奇偶情况 + 数学：奇偶不同为偶
        MOD = 10**9 + 7
        odd, even = 0,1
        subarrays = 0
        total = 0
        for num in arr:
            total += num
            subarrays += odd if total%2 == 0 else even
            if total%2 == 0:
                even += 1
            else:
                odd += 1
        return subarrays%MOD
```

### 974. 和可被 K 整除的子数组

```python
class Solution(object):
    def subarraysDivByK(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        cnt = defaultdict(int)
        ans = s = 0
        for x in nums:
            cnt[s] += 1# s = 0 从0开始也要算
            s = (s + x)%k
            ans += cnt[s]
        return ans
```

### 523. 连续的子数组和

```python
class Solution(object):
    def checkSubarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """
        n = len(nums)

        total = nums[0]
        cnt = {0}
        for x in nums[1:]:
            if (total + x)%k in cnt:
                return True
            cnt.add(total%k)
            total += x
        return False
```