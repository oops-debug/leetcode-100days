### 2078. 两栋颜色不同且距离最远的房子

o(n^2)解法

```python
class Solution(object):
    def maxDistance(self, colors):
        """
        :type colors: List[int]
        :rtype: int
        """
        n = len(colors)
        ans = 0
        for i in range(n):
            for j in range(i+1,n):
                if colors[i] != colors[j]:
                    ans = max(ans,j-i) 
        return ans 
```

o(n)解法

```python
class Solution(object):
    def maxDistance(self, colors):
        """
        :type colors: List[int]
        :rtype: int
        """
        n = len(colors)
        ans = 0
        ansr = ansl = 0
        c = colors[0]
        for i in range(n):
            if c != colors[n-1-i]:
                ans= max(n-i-1,ans)
        c = colors[-1]
        for j in range(n):
            if c != colors[j]:
                ans = max(n-j-1,ans)
        return ans
```


