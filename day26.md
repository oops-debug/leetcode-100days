### 438.找到字符串中所有的字母异位词
```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        lenth = len(p)
        cnt1 = [0] * 26
        cnt2 = [0]*26
        ans = []
        for i in p:
            cnt1[ord(i)-ord('a')] += 1
        left = 0 
        for right,c in enumerate(s):
            cnt2[ord(c)-ord('a')] += 1
            while cnt2[ord(c)-ord('a')] > cnt1[ord(c)-ord('a')]:
                cnt2[ord(s[left])-ord('a')] -= 1
                left += 1
            if cnt1 == cnt2:# 判断可以优化
                ans.append(left)
        return ans
```

```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        lenth = len(p)
        cnt1 = [0] * 26
        ans = []
        for i in p:
            cnt1[ord(i)-ord('a')] += 1
        left = 0 
        for right,c in enumerate(s):
            cnt1[ord(c)-ord('a')] -= 1
            while  cnt1[ord(c)-ord('a')]<0:
                cnt1[ord(s[left])-ord('a')] += 1
                left += 1
            # 长度相等并且每个字母不超量
            if right-left+1 == lenth:
                ans.append(left)
        return ans
```
