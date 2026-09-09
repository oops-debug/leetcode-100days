# 时隔两个月02天，决定从hot100开始刷
## 20. 有效的括号---栈的经典题目
两种方法，实际上就一种，只是一个是左括号入栈，所以哈希需要是右：左，一个是右括号入栈，所以哈希是左：右
```python
class Solution:
    def isValid(self, s: str) -> bool:
        # mp = {')': '(', ']': '[', '}': '{'}
        mp = {'(': ')', '[': ']', '{': '}'}
        st = []
        for c in s:
            if c in mp:
                st.append(mp[c])
            elif not st or st.pop() != c :
                return False
        return not st
```
```python
class Solution:
    def isValid(self, s: str) -> bool:
        if len(s) % 2:  # s 长度必须是偶数
            return False
        mp = {')': '(', ']': '[', '}': '{'}
        st = []
        for c in s:
            if c not in mp:  # c 是左括号
                st.append(c)  # 入栈
            elif not st or st.pop() != mp[c]:  # c 是右括号
                return False  # 没有左括号，或者左括号类型不对
        return not st  # 所有左括号必须匹配完毕
```