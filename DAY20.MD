### 739.每日温度
```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        tem_queue = []
        n = len(temperatures)
        res = [0]*n
        for i,t in enumerate(temperatures):
            while tem_queue and temperatures[tem_queue[-1]]<t:
                j = tem_queue.pop()
                res[j] = i-j
            tem_queue.append(i)
        return res
```
