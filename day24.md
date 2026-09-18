### 盛最多水的容器
看别人评论做出来的，核心是从两端向中间逼近，哪个短就移动哪个
```python
class Solution:
    def maxArea(self, height: list[int]) -> int:
        lenth = len(height)
        left = 0 
        right = lenth-1
        ans = 0
        while left != right:
            ans = max(min(height[left],height[right])*(right-left),ans)
            if height[left]<=height[right] :
                left += 1 
            else :
                right-=1
        return ans
```

### 15.三数之和
```python
class Solution:
    def threeSum(self, nums: list[int]) -> list[list[int]]:
        nums.sort()
        ans=[]
        n = len(nums)
        for i in range(n-2):
            x = nums[i]
            if i>0 and x == nums[i-1]:
                continue
            if x + nums[i+1] + nums[i+2]>0:
                break
            if x + nums[-2] + nums[-1]<0:
                continue
            j = i + 1
            k = n - 1
            while j < k:
                s = nums[j] + nums[k] + x
                if s > 0:
                    k -= 1
                elif s < 0:
                    j += 1
                else:
                    ans.append([x,nums[j],nums[k]])
                    j += 1
                    while j<k and nums[j] == nums[j-1]:
                        j = j+1
                    k -= 1
                    while k>j and nums[k] == nums[k+1]:
                        k = k - 1
        return ans
```

```python
class Solution:
    def threeSum(self, nums: list[int]) -> list[list[int]]:
        nums.sort()
        ans=[]
        n = len(nums)
        for i in range(n-2):
            x = nums[i]
            if i>0 and x == nums[i-1]:
                continue
            if x + nums[i+1] + nums[i+2]>0:
                break
            if x + nums[-2] + nums[-1]<0:
                continue
            j = i + 1
            k = n - 1
            while j < k:
                s = nums[j] + nums[k] + x
                if s > 0:
                    k -= 1
                elif s < 0:
                    j += 1
                else:  # 三数之和为 0
                    # j = i+1 表示刚开始双指针，此时 j 左边没有数字
                    # nums[j] != nums[j-1] 说明与上一轮循环的三元组不同
                    if j == i + 1 or nums[j] != nums[j - 1]:
                        ans.append([x, nums[j], nums[k]])
                    j += 1
                    k -= 1

        return ans
```