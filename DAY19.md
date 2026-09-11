### 394.字符串解码
#### 法一：栈
```python
class Solution:
    def decodeString(self, s: str) -> str:
        st = [] # 保存现在的字符串和后面的字符要repeat的次数
        num = 0
        repeat = 0
        cur_str = []
        for cur in s:
            if cur.isdigit():
                num = num * 10 + int(cur)# 不一定是个位数
            elif cur is '[':
                st.append((num,cur_str))
                cur_str = []
                num = 0
            elif cur.isalpha():
                cur_str.append(cur)
            elif cur is ']':
                repeat, pre_str = st.pop()
                cur_str = pre_str + cur_str*repeat
        return "".join(cur_str)
```
#### 递归
