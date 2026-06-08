# 常用枚举技巧
## 枚举中间
### 3583. 统计特殊三元组


```python
class Solution(object):
    def specialTriplets(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        cnt1 = defaultdict(int)
        cnt2 = defaultdict(int)
        for num in nums:
            cnt2[num] += 1
        ans = 0
        MOD = 10**9 + 7 # 10e8+7是浮点型
        for i in range(0,len(nums)):
            cnt2[nums[i]]-=1
            ans += cnt1[2*nums[i]]*cnt2[2*nums[i]]
            cnt1[nums[i]]+=1
        return ans%(MOD)
```

### 1930. 长度为 3 的不同回文子序列

枚举中间，维护前缀后缀：前缀因为有不需要考虑重复直接用set,后缀因为需要考虑重复，用哈希或者数组

要求不能重复：用set维护答案1/3重复，所以只用维护两个字母
```python
class Solution(object):
    def countPalindromicSubsequence(self, s):
        """
        :type s: str
        :rtype: int
        """
        cnt1 = set()
        cnt2 = [0]*26
        answer = set()
        for i in range(26):# 时间复杂度O(26n)
            cnt2[i] = s.count(chr(ord('a')+i))
        for word in s:
            cnt2[ord(word)-ord('a')] -= 1
            for j in cnt1:
                answer.add(word+j) if cnt2[ord(j)-ord('a')] >0 else 0
                
            cnt1.add(word)
        return len(answer)
```

```python
class Solution(object):
    def countPalindromicSubsequence(self, s):
        """
        :type s: str
        :rtype: int
        """
        cnt1 = set()
        cnt2 = Counter(s)# 时间复杂度低o(n)
        answer = set()
        for word in s:
            cnt2[word] -= 1
            for j in cnt1:
                if cnt2[j] >0:
                    answer.add(word+j) 
            cnt1.add(word)
        return len(answer)
```
> [!TIP]
> 位变换方法
### 3128. 直角三角形

zip(*x)行列转换

zip(a,b)ab组合一一对应

```python
class Solution(object):
    def numberOfRightTriangles(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        # for j in range(len(grid[0])):
        #     for i in range(len(grid)):
        #         col[j] += grid[i][j]
        col_sum = [sum(col) - 1 for col in zip(*grid)]
        ans = 0
        for nums in grid:
            cnt = sum(nums)-1
            # if cnt<2:
            #     continue
            # for i in range(len(nums)):
            #     if nums[i]:
            #         ans+=(col[i]-1)*(cnt-1)
            ans += cnt*sum(cs for x,cs in zip(nums,col_sum) if x)
        return ans
```